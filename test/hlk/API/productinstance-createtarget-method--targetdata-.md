---
title: ProductInstance.CreateTarget Method (TargetData)
description: ProductInstance.CreateTarget Method (TargetData)
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 31A00F66-F9CC-44AC-8275-7C2A6BCEFBB8
author: aahi
ms.author: aahi
ms.date: 10/15/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-oem
---

# ProductInstance.CreateTarget Method (TargetData)

>[!WARNING]
>  This functionality is being deprecated.

 

This method creates a target from [TargetData](targetdata-class.md), and adds it to this product instance.

Calls the overload method and creates the [Target](target-class.md) without adding tests.

**Namespace:** Microsoft.Windows.Kits.Hardware.ObjectModel

**Assembly:** Microsoft.Windows.Kits.Hardware.ObjectModel (in Microsoft.Windows.Kits.Hardware.ObjectModel)

## <span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>Syntax


**C#**

`public Target CreateTarget (`

          `TargetData data`

`)`

## <span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


*data*

     The [TargetData](targetdata-class.md) to use to create the target.

## <span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>Return Value


The new [Target](target-class.md) object that was created.

## <span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>Remarks


Any target has to be a child of a [TargetFamily](targetfamily-class.md). Any hardware IDs found in the target data will be used to find a TargetFamily. If no TargetFamily is found that contains one of the hardware IDs, a new TargetFamily is created. In the case that a [TargetException](targetexception-class.md) is thrown due to the refresh failing, verify the database connection is valid and that the target device has not been removed and is still present on the system if connected to a database project; if the hardware/driver is present and available, additionally waiting for a few minutes for the data to become available and/or rebooting the client system, then retrying this call may resolve the issue.

## <span id="Thread_Safety"></span><span id="thread_safety"></span><span id="THREAD_SAFETY"></span>Thread Safety


Any public static members of this type are thread safe. Any instance members are not guaranteed to be thread safe.

 

 






