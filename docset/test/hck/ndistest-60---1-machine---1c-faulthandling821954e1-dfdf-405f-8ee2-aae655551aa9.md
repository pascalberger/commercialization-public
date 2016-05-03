---
author: joshbax-msft
title: NDISTest 6.0 - 1 Machine - 1c\_FaultHandling
description: NDISTest 6.0 - 1 Machine - 1c\_FaultHandling
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 7ab82591-dc5e-469b-88d8-d1683412b78c
---

# NDISTest 6.0 - 1 Machine - 1c\_FaultHandling


This automated test uses a fault injection feature of NDIS. Each loop will set bits in the registry for the driver under test. These bits will cause NDIS to fail specific NDIS calls. The registry value name is NdisDriverVerifyFlags. The loop, value, and NDIS call are listed below:

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Loop</th>
<th>Value</th>
<th>NDIS Call</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>0x001</p></td>
<td><p>NdisMAllocateMapRegisters</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p>0x002</p></td>
<td><p>NdisMRegisterInterrupt</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p>0x004</p></td>
<td><p>NdisMAllocateSharedMemory</p></td>
</tr>
<tr class="even">
<td><p>3</p></td>
<td><p>0x010</p></td>
<td><p>NdisMMapIoSpace</p></td>
</tr>
<tr class="odd">
<td><p>4</p></td>
<td><p>0x020</p></td>
<td><p>NdisMRegisterIoPortRange</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p>0x040</p></td>
<td><p>Read NdisGetSetBusConfigSpace</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p>0x080</p></td>
<td><p>Write NdisGetSetBusConfigSpace</p></td>
</tr>
<tr class="even">
<td><p>7</p></td>
<td><p>0x100</p></td>
<td><p>NdisMInitializeScatterGatherDma</p></td>
</tr>
</tbody>
</table>

 

The driver should not load unless it does not call the particular function. This test is successful as long the driver does not crash the system. During each test loop, after the driver fails to load the registry is cleared and the driver is loaded normally to be sure it still works.

## Test details


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Associated requirements</strong></p></td>
<td><p>Device.Network.LAN.Base.NDISRequirements</p>
<p>[See the device hardware requirements.](http://go.microsoft.com/fwlink/p/?linkid=254483)</p></td>
</tr>
<tr class="even">
<td><p><strong>Platforms</strong></p></td>
<td><p>Windows 7 (x64) Windows 7 (x86) Windows 8 (x64) Windows 8 (x86) Windows Server 2012 (x64) Windows Server 2008 R2 (x64) Windows 8.1 x64 Windows 8.1 x86 Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected run time</strong></p></td>
<td><p>~5 minutes</p></td>
</tr>
<tr class="even">
<td><p><strong>Categories</strong></p></td>
<td><p>Certification Functional</p></td>
</tr>
<tr class="odd">
<td><p><strong>Type</strong></p></td>
<td><p>Automated</p></td>
</tr>
</tbody>
</table>

 

## Running the test


Before you run the test, complete the test setup as described in the test requirements: [LAN Testing Prerequisites](lan-testing-prerequisites.md).

## Troubleshooting


For troubleshooting information, see [Troubleshooting LAN Testing](troubleshooting-lan-testing.md).

## More information


### Parameters

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
<td><p>queryTestDeviceID</p></td>
<td><p>The ID of the test device.</p>
<p>Example: //Devnode/DeviceID</p></td>
</tr>
</tbody>
</table>

 

### Command syntax

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Command</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>[WTTRunWorkingDir]\ndistest\bin\ndtest.exe /auto /client /dvi /u /target:Miniport /tc:[queryTestDeviceID] /script:{1c_FaultHandling.wsf}</strong></p></td>
<td><p>Runs the test.</p></td>
</tr>
</tbody>
</table>

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20NDISTest%206.0%20-%201%20Machine%20-%201c_FaultHandling%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



