---
title: Autodetect the Printer's Hard Drive for PPD
author: windows-driver-content
description: Autodetect the Printer's Hard Drive for PPD
ms.assetid: 0f2eba5c-1a05-4aaf-8780-266d2339570e
keywords:
- autodetecting printer hard drive WDK printer autoconfiguration
- PPD files WDK autoconfiguration , autodetecting hard drive
- in-box autoconfiguration support WDK printer , autodetecting hard drive
- detecting printer hard drive
- hard drive autodetection WDK printer
ms.author: windowsdriverdev
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Autodetect the Printer's Hard Drive for PPD


Add entries to the GDL file for any hard drive-related features in your PPD file. You can do this by creating a corresponding feature construct in the GDL file using the same technique shown in the previous example. The following GDL construct automatically detects whether a hard disk is installed.

```
*% The GDL parser merges this feature definition with the 
*% corresponding feature construct in the GPD file
*Feature: PrinterHardDisk
{
  *FeatureType: PRINTER_PROPERTY

  *BidiQuery: PrinterHardDisk
  {
     *QueryString: "\Printer.Configuration.HardDisk:Installed"
  }
  *BidiResponse: PrinterHardDisk
  {
     *ResponseType: BIDI_BOOL
     *ResponseData: ENUM_OPTION (PrinterHardDisk)
  }
  *Option: FALSE
  {
     *BidiValue: BOOL(FALSE)
  }
  *Option: TRUE
  {
     *BidiValue: BOOL(TRUE)
  }
}
```

 

 




