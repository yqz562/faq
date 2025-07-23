---
layout: default-layout
title: Solve Page Freeze - DBR Mobile FAQs
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, ios, android, freeze, page, license
description: Why does the page sometimes freeze when I start the scanner? - DBR Mobile FAQs.
needAutoGenerateSidebar: true
---

# Why does the page sometimes freeze when I start the scanner?

[<< Back to FAQ index](index.md)

Before a barcode reader instance can be created, a one-time connection for **license validation** must occur when the app initializes—or whenever the license is set prior to the barcode reader’s instantiation. This license check may take a second to complete, potentially causing a temporary freeze in the UI.

A common cause of this issue is **calling `initLicense` multiple times** in the same process.

## iOS

For iOS, the method is [`LicenseManager.initLicense()`]({{ site.dcvb_ios_api }}license/license-manager.html#initlicense).  
We’ve seen cases where developers call this method in both the `AppDelegate` and `ViewController`, leading to conflicts.

✅ **Recommendation**: Call `initLicense` only once—preferably in the `AppDelegate`.

## Android

For Android, the method is `BarcodeReader.initLicense()`.  
To ensure it’s not being called more than once, we suggest stepping through your code using a debugger.

✅ **Recommendation**: Call `initLicense` only once during app initialization.

---
