---
author: joshbax-msft
title: WLAN Scan Tests - ScanMix4 - Reliability
description: WLAN Scan Tests - ScanMix4 - Reliability
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 82d06b35-f663-4375-ab99-2969a88c43d0
---

# WLAN Scan Tests - ScanMix4 - Reliability


## Test details


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Associated requirements</strong></p></td>
<td><p>Device.Network.WLAN.Base.MeetScanAndConnReq Device.Network.WLAN.CSBBase.MeetScanAndConnReq Device.Network.WLAN.CSBNLO.SupportNetworkListOffload Device.Network.WLAN.NLO.SupportNetworkListOffload</p>
<p>[See the device hardware requirements.](http://go.microsoft.com/fwlink/p/?linkid=254483)</p></td>
</tr>
<tr class="even">
<td><p><strong>Platforms</strong></p></td>
<td><p>Windows RT (ARM-based) Windows 8 (x64) Windows 8 (x86) Windows RT 8.1 Windows 8.1 x64 Windows 8.1 x86</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected run time</strong></p></td>
<td><p>~6 minutes</p></td>
</tr>
<tr class="even">
<td><p><strong>Categories</strong></p></td>
<td><p>Certification Reliability</p></td>
</tr>
<tr class="odd">
<td><p><strong>Type</strong></p></td>
<td><p>Automated</p></td>
</tr>
</tbody>
</table>

 

## Running the test


Before you run the test, complete the test setup as described in the test requirements: [Wireless LAN (802.11) Testing Prerequisites](wireless-lan--80211--testing-prerequisites.md).

This test performs the following actions:

-   Configure two routers, that are named Router 0 and Router 1, as follows:

    -   Router 0 – 2.4Ghz : WPA2ENTERPRISE / AES /G/Channel 1

    -   Router 0 – 5Ghz : WPA2PSK / AES /N/Channel 36

    -   Router 1 – 2.4Ghz : WPA2ENTERPRISE / TKIP /G/Channel 9

    -   Router 1 – 5Ghz : WPA2PSK / TKIP /N/Channel 36

-   Perform a scan by using a public API.

-   Validate Router 0. Router 1 2.4 GHz and 5 GHz are available in the scan list.

-   Perform a scan by using a private API.

-   Validate Router 0. Router 1 2.4 GHz and 5 GHz are available in the scan list.

## Troubleshooting


For troubleshooting information, see [Troubleshooting Wireless LAN (802.11) Tests](troubleshooting-wireless-lan--80211--tests.md)

## More information


### Command syntax

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TestDeviceSupports5ghz</strong></p></td>
<td><p>Determines whether or not the device supports 5 GHz.</p>
<p>Default value: True</p></td>
</tr>
<tr class="even">
<td><p><strong>AP1Password</strong></p></td>
<td><p>The root password for the first physical access point.</p>
<p>Default value: password</p></td>
</tr>
<tr class="odd">
<td><p><strong>AP1IPAddress</strong></p></td>
<td><p>The IP address of the WAN port of the first physical access point.</p>
<p>Default value: 192.168.2.2</p></td>
</tr>
<tr class="even">
<td><p><strong>AP2Password</strong></p></td>
<td><p>The root password for the second physical access point.</p>
<p>Default value: password</p></td>
</tr>
<tr class="odd">
<td><p><strong>AP2IPAddress</strong></p></td>
<td><p>The root password for the second physical access point.</p>
<p>Default value: 192.168.2.3</p></td>
</tr>
<tr class="even">
<td><p><strong>EnableTracing</strong></p></td>
<td><p>Default value: No</p></td>
</tr>
</tbody>
</table>

 

## Related topics


[Wireless LAN (802.11) Tests](wireless-lan--80211--tests.md)

 

 






