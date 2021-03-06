---
title: INF Requirements for NDKPI
description: The INF file for a miniport driver that supports Network Direct kernel (NDK) must meet the following requirements.
ms.assetid: 1399CEB8-82A5-4F91-833E-66FC5A5663C7
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# INF Requirements for NDKPI


The INF file for a miniport driver that supports Network Direct kernel (NDK) must meet the following requirements.

-   The miniport driver's INF file must specify an NDIS upper range value of "ndis5" in order for Windows components to discover and use the NDK-capable miniport adapters that are serviced by the driver. This value is specified as follows:

    ``` syntax
    HKR, Ndi\Interfaces, UpperRange, 0, "ndis5"
    ```

-   The INF file must specify the **\*NetworkDirect** keyword value as follows. Once the driver is installed, administrators can update the **\*NetworkDirect** keyword value in the **Advanced** property page for the adapter. 

    **Note**   The miniport driver is automatically restarted after a change is made in the **Advanced** property page for the adapter.

     

    ``` syntax
    HKR, Ndi\Params\*NetworkDirect,        ParamDesc,  0, "NetworkDirect Functionality"
    HKR, Ndi\Params\*NetworkDirect,        Type,       0, "enum"
    HKR, Ndi\Params\*NetworkDirect,        Default,    0, "1"
    HKR, Ndi\Params\*NetworkDirect\enum,   "0",        0, "Disabled"
    HKR, Ndi\Params\*NetworkDirect\enum,   "1",        0, "Enabled"
    ```


-   The INF file must specify the **\*NetworkDirectTechnology** keyword value as follows. Once the driver is installed, administrators can update the **\*NetworkDirectTechnology** keyword value in the **Advanced** property page for the adapter. The enumerations are mutually exclusive, meaning  the selection of a NetworkDirectTechnology value excludes all others.  This allows for the Platform to define strict  device behavior.  For devices where multiple transports can be supported concurrently, the **Undefined** allows for device specific behavior, such as retry/fallback to multiple transports.

    **Note**   The miniport driver is automatically restarted after a change is made in the **Advanced** property page for the adapter.

    ```
    HKR, Ndi\Params\*NetworkDirectTechnology,        ParamDesc,  0,  "NetworkDirect Technology"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Default,    0,  "1"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Type,       0,  "enum"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   1,          0,  "Undefined"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   2,          0,  "iWARP"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   3,          0,  "InfiniBand"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   4,          0,  "RoCE"
    HKR, Ndi\Params\*NetworkDirectTechnology\enum,   5,          0,  "RoCEv2"
    HKR, Ndi\Params\*NetworkDirectTechnology,        Optional,   0,  "1"
    ```

    For more information about advanced properties, see [Specifying Configuration Parameters for the Advanced Properties Page](specifying-configuration-parameters-for-the-advanced-properties-page.md).

    For more information about using standardized INF keywords, see [Standardized INF Keywords for Network Devices](standardized-inf-keywords-for-network-devices.md).

## Related topics


[Network Direct Kernel Provider Interface (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 
