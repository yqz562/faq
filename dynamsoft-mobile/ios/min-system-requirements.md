---
layout: default-layout
title: Minimum system requirements - DBR iOS FAQs.
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, ios, requirements
description: What are the minimum system requirements of Dynamsoft Barcode Reader iOS? - DBR iOS FAQs.
needAutoGenerateSidebar: true
---

# What are the minimum system requirements of Dynamsoft Barcode Reader iOS?

[<< Back to FAQ index](index.md)

For iOS, DBR supports the following:

* Supported OS: **iOS 11** or higher (**iOS 13** and higher recommended).
* Supported ABI: **arm64** and **x86_64**.
* Development Environment: Xcode 13 and above (Xcode 14.1+ recommended).

Please note that the **armv7** architecture is not supported. If you are doing a general build for all iOS devices, make sure to exclude it in the build settings.

The x86_64 architecture usually coresponds to the simulator. Please note that in order to use the simulator, you must use the **xcframework** instead of the **framework**.