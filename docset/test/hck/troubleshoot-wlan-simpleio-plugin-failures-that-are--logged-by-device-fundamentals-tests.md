---
author: joshbax-msft
title: Troubleshoot WLAN SimpleIO plugin failures that are logged by Device Fundamentals tests
description: Troubleshoot WLAN SimpleIO plugin failures that are logged by Device Fundamentals tests
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: adfde9af-dfa9-4ddd-8e06-aa5ef76ee5af
---

# Troubleshoot WLAN SimpleIO plugin failures that are logged by Device Fundamentals tests


Device Fundamentals tests in Windows Hardware Certification Kit (Windows HCK) and [Windows Drivers Kit (WDK)](http://go.microsoft.com/fwlink/p/?linkid=296487) use [Windows Device Testing Framework (WDTF)](http://go.microsoft.com/fwlink/p/?linkid=296367)[SimpleIO plugins](http://go.microsoft.com/fwlink/p/?linkid=296486) to test device-specific IO when they run. If a WDTF plugin exists for the type of device being tested, then the tests use the [IWDTFSimpleIOStressAction2 interface](http://go.microsoft.com/fwlink/p/?linkid=299599) to test I/O on the device.

This article contains information that can help with troubleshooting failures that are logged by the WDTF WLAN SimpleIO plug-in when it is used to test IO on wireless network adapters during device and system testing in WDK and Windows HCK.

## <a href="" id="configreq"></a>Configuration requirements


The WLAN SimpleIO plug-in requires a basic WPA2-PSK wireless network that uses AES that it can connect to when it runs. The SSID and password of the wireless network must be passed in as parameters to the tests that require them. These parameters are named as follows in the tests that require them: **Wpa2PskAesSsid** and **Wpa2PskPassword**. The default values of the two parameters are **kitstestssid** and **password**, respectively.

## <a href="" id="ov"></a>Test coverage overview


The WLAN SimpleIO plug-in performs the following tests on the wireless adapter under test:

1.  Finds the Wlan interface that is under test by calling the [WlanEnumInterfaces function](http://go.microsoft.com/fwlink/p/?linkid=296597).

2.  Deletes the test profile that is named WDTFWlanTestProfile (if it exists) by calling the [WlanGetProfile() function](http://go.microsoft.com/fwlink/p/?linkid=296598) and the [WlanDeleteProfile() function](http://go.microsoft.com/fwlink/p/?linkid=296599).

3.  Creates a new test profile named **WDTFWlanTestProfile** by calling the [WlanSetProfile() function](http://go.microsoft.com/fwlink/p/?linkid=296600) and by using a profile XML. The profile uses the SSID and password of the wireless network as input parameters to the test.

4.  Connects to the newly created profile by calling the [WlanConnect() function](http://go.microsoft.com/fwlink/p/?linkid=296601). Expect to receive a *connect complete* notification in 30 seconds.

5.  Checks for connectivity by calling the [INetworkListManager::GetConnectivity method](http://go.microsoft.com/fwlink/p/?linkid=296604) of the [Network List Manager](http://go.microsoft.com/fwlink/p/?linkid=296603) API, and looks for [NLM\_CONNECTIVITY enumeration](http://go.microsoft.com/fwlink/p/?linkid=296605) NLM\_CONNECTIVITY\_IPV4\_INTERNET or NLM\_CONNECTIVITY\_IPV4\_LOCALNETWORK flags to be set. The plug-in calls the **GetConnectivity()** function several times (if required) as it waits for a connection, before it eventually times out and reports an error.

6.  Calls the [GetAdaptersInfo() function](http://go.microsoft.com/fwlink/p/?linkid=296606) to determine the gateway address that corresponds to the test adapter.

7.  Opens an ICMP handle by calling [IcmpCreateFile() function](http://go.microsoft.com/fwlink/p/?linkid=296607), and calls an internal function in a loop for several minutes that pings the IPv4 gateway address (by using the [IcmpSendEcho() function](http://go.microsoft.com/fwlink/p/?linkid=296608) with one-second timeout) 500 times each time it is called, and logs an error message if at any time it is called, the failure rate is &gt;10%.

8.  Disconnects from the network by calling the [WlanDisconnect() function](http://go.microsoft.com/fwlink/p/?linkid=296602).

9.  Deletes the test profile by calling the [WlanGetProfile() function](http://go.microsoft.com/fwlink/p/?linkid=296598) and the [WlanDeleteProfile() function](http://go.microsoft.com/fwlink/p/?linkid=296599).

## <a href="" id="guidance"></a>Troubleshooting guidance


### Identify failures that are logged by the WLAN SimpleIO plugin

The error messages logged by the plug-in will contain the text “WirelessPlugin:”. The text that immediately follows “WirelessPlugin:” provides more context about the errors. For example:

``` syntax
WDTF_SIMPLE_IO            : ERROR :  - Open(802.11n USB Wireless LAN Card USB\VID_XXXX&PID_XXXX\5&35DEE9D9&0&5 ) Failed : WirelessPlugin: ConnectToTestProfile() - Failed to connect to test profile; Reason string: "The specific network is not available." HRESULT=0x80004005
```

### General troubleshooting guidance

We recommend that you follow troubleshooting steps in the listed order:

1.  Review the test documentation to understand the test scenario.

2.  Review [Test coverage overview](#ov) to understand how the plugin tests a device or driver.

3.  Carefully review log entries that precede the error message, and the error message itself, to understand the test scenario and the reason for the failure.

4.  Troubleshoot the router setup. Make sure that you can manually connect to the router, that you can ping the gateway address after making the connection, and that the router is in range to the test computer. If the router fails any of these tests, reset the router.

5.  Enable tracing in the test driver and review driver traces from the time when the test logged the error(s).

6.  Enable **WLAN OS tracing** and review traces that are logged from the time when the logged the error(s). For more information about WLAN OS tracing, see [Tools for Troubleshooting using Network Tracing in Windows 7](http://go.microsoft.com/fwlink/p/?linkid=296757).

In some cases, it is helpful to run the failing test manually from a command line (without using Windows HCK or WDK), and then reviewing the plug-in’s WPP traces. See [How to run tests from the command line](#cmd) and [View WLAN plug-in traces](#view).

## <a href="" id="cmd"></a>How to run tests from the command line


We recommend that you use a Windows HCK Client to run tests manually because Windows HCK clients have WDTF installed on them. Follow the steps in Troubleshooting Device Fundamentals Reliability Testing by using the Windows HCK. Enable Driver Verifier on Ndis.sys and the test Wi-Fi driver.

## <a href="" id="view"></a>View WLAN plug-in traces


The WLAN plugin uses WPP tracing to trace information and errors that you might find useful when you investigate failures that are logged by the WLAN plug-in. See [Collect and View Windows Device Testing Framework (WDTF) Traces](collect-and-view-windows-device-testing-framework--wdtf--traces.md) for instructions on how to collect and view WDTF traces.

**Note**  
**WDTF\_Action\_SimpleIO\_Wireless** is the name of the provider that you can use for filtering.

 

## Sample trace output


``` syntax
                               -->this(047BB318):?FinalConstruct@CWirelessImpl@@QEAAJXZ(void)
                               <--this(047BB318):?FinalConstruct@CWirelessImpl@@QEAAJXZ(): S_OK
                               o->this(047BB318):?SetTarget@CWirelessImpl@@UEAAJPEAUITarget@@UtagVARIANT@@@Z(pMainTarget = 0476BBAC, MoreTargets = 8)
                                    INFO:Calling WlanOpenHandle() function
                                    INFO:Calling WlanEnumInterfaces() function to find wlan interface under test: N300 USB Network Adapter" ({4138C082-E821-433C-ABB8-6FF864BF80B5})"
                                    INFO:Found 1 wlan interfaces in total
                                    INFO:Processing wlan interface: N300 USB Network Adapter""
                                    INFO:Found the wlan interface under test!
                                    INFO:Interface information: Interface Guid: {4138C082-E821-433C-ABB8-6FF864BF80B5}; Interface State: disconnected""
                               o<-this(047BB318):?SetTarget@CWirelessImpl@@UEAAJPEAUITarget@@UtagVARIANT@@@Z(): S_OK
           o->this(047BB318):?Open@CWirelessImpl@@UEAAJXZ(void)
                INFO:Calling WlanOpenHandle() function
                -->this(047BB318):?FindAndDeleteTestProfile@CWirelessImpl@@AEAAJXZ(void)
                     INFO:Test profile WDTFWlanTestProfile" doesn't exist"
                o<-this(047BB318):?FindAndDeleteTestProfile@CWirelessImpl@@AEAAJXZ(): S_OK
                -->this(047BB318):?CreateTestProfile@CWirelessImpl@@AEAAJXZ(void)
                     INFO:Calling WlanSetProfile() with a profile XML to create a profile with name: WDTFWlanTestProfile"
                o<-this(047BB318):?CreateTestProfile@CWirelessImpl@@AEAAJXZ(): S_OK
                -->this(047BB318):?ConnectToTestProfile@CWirelessImpl@@AEAAJXZ(void)
                     INFO:Calling WlanRegisterNotification() to get notified of connect complete event
                     INFO:Calling WlanConnect() to connect to test profile with name: WDTFWlanTestProfile""
                     INFO:Waiting to receive connect complete notification
                     INFO:Received connect complete notification: 0
                     INFO:Calling WlanRegisterNotification() to unregister from notifications
                o<-this(047BB318):?ConnectToTestProfile@CWirelessImpl@@AEAAJXZ(): S_OK
                INFO:Calling an internal helper function to check for the connectivity state of the network connection
                -->this(047BB318):?CheckForConnectivity@CWirelessImpl@@AEAAJPEA_N@Z(void)
                     INFO:Creating an instance of the NLM COM object
                     INFO:Calling NLM GetNetworkConnections() to get a list of network connections
                     INFO:Iterating through the network connections found looking for the connection corresponding to the test adapter ({4138C082-E821-433C-ABB8-6FF864BF80B5})
                     INFO:Calling NLM GetAdapterId() on a network connection found
                     INFO:Calling NLM GetAdapterId() on a network connection found
                     INFO:Found a network connection using the test adapter!
                     INFO:Calling NLM GetConectivity() on a network connection using the test adapter
                     INFO:NLM GetConectivity() reported the following connectivity state: 66
                     INFO:NLM GetConectivity() reported IPv4 connectivity!
                o<-this(047BB318):?CheckForConnectivity@CWirelessImpl@@AEAAJPEA_N@Z(): S_OK
                -->this(047BB318):?RefreshIPInfo@CWirelessImpl@@AEAAJXZ(void)
                     INFO:Calling GetAdaptersInfo() function to find IP address info for adapter {4138C082-E821-433C-ABB8-6FF864BF80B5}""
                     INFO:Found the adapter we are looking for!
                     INFO:Adapter Info: Index: 4, IPv4 Address: 192.168.1.147, Gateway Address: 192.168.1.1
                o<-this(047BB318):?RefreshIPInfo@CWirelessImpl@@AEAAJXZ(): S_OK
                INFO:Calling IcmpCreateFile() function
                INFO:Pinging gateway (192.168.1.1) 10 times
                -->this(047BB318):?TestPingGateway@CWirelessImpl@@AEAAJHH@Z(numPings: 10)
                     INFO:Calling IcmpSendEcho() to ping gateway (192.168.1.1) 10 times with a random input buffer of size 255 and a timeout value of 1000 milliseconds
                o<-this(047BB318):?TestPingGateway@CWirelessImpl@@AEAAJHH@Z(): S_OK
           o<-this(047BB318):?Open@CWirelessImpl@@UEAAJXZ(): S_OK
           o->this(047BB318):?RunIO@CWirelessImpl@@UEAAJXZ(void)
                -->this(047BB318):?TestPingGateway@CWirelessImpl@@AEAAJHH@Z(numPings: 500)
                     INFO:Calling IcmpSendEcho() to ping gateway (192.168.1.1) 500 times with a random input buffer of size 255 and a timeout value of 1000 milliseconds
                o<-this(047BB318):?TestPingGateway@CWirelessImpl@@AEAAJHH@Z(): S_OK
           o<-this(047BB318):?RunIO@CWirelessImpl@@UEAAJXZ(): S_OK
           o->this(047BB318):?RunIO@CWirelessImpl@@UEAAJXZ(void)
                -->this(047BB318):?TestPingGateway@CWirelessImpl@@AEAAJHH@Z(numPings: 500)
                     INFO:Calling IcmpSendEcho() to ping gateway (192.168.1.1) 500 times with a random input buffer of size 255 and a timeout value of 1000 milliseconds
                o<-this(047BB318):?TestPingGateway@CWirelessImpl@@AEAAJHH@Z(): S_OK
           o<-this(047BB318):?RunIO@CWirelessImpl@@UEAAJXZ(): S_OK
...
...
...
           o->this(047BB318):?Close@CWirelessImpl@@UEAAJXZ(void)
                -->this(047BB318):?DisconnectFromTestProfile@CWirelessImpl@@AEAAJXZ(void)
                     INFO:Calling WlanDisconnect() to disconnect
                o<-this(047BB318):?DisconnectFromTestProfile@CWirelessImpl@@AEAAJXZ(): S_OK
                -->this(047BB318):?FindAndDeleteTestProfile@CWirelessImpl@@AEAAJXZ(void)
                     INFO:Calling WlanDeleteProfile() to delete the previously created test profile with name WDTFWlanTestProfile""
                o<-this(047BB318):?FindAndDeleteTestProfile@CWirelessImpl@@AEAAJXZ(): S_OK
           o<-this(047BB318):?Close@CWirelessImpl@@UEAAJXZ(): S_OK
```

## Related topics


[Troubleshooting Device Fundamentals Reliability Testing by using the Windows HCK](troubleshooting-device-fundamentals-reliability-testing-by-using-the-windows-hck.md)

[Troubleshooting Windows HCK](troubleshooting-windows-hck.md)

[Windows HCK Support](windows-hck-support.md)

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20Troubleshoot%20WLAN%20SimpleIO%20plugin%20failures%20that%20are%20%20logged%20by%20Device%20Fundamentals%20tests%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




