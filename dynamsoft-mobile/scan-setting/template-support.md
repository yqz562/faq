---
layout: default-layout
title: Common Issues & Settings - DBR Mobile FAQs
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, android, ios, freeze, license, template, scanner settings
description: Solve page freeze issue on iOS and learn how to import settings from Barcode Scanner X on Android.
needAutoGenerateSidebar: true
---

# Common Issues & Settings

[<< Back to FAQ index](index.md)

---

## iOS: Why does the page sometimes freeze when I start the scanner?

Before a barcode reader instance can be created, a one-time license validation needs to occur when the app initializes (or whenever the license is set before the reader instance is created). Occasionally, this process may take a second to complete and could cause the UI to appear frozen.

A common cause is calling [`LicenseManager.initLicense()`]({{ site.dcvb_ios_api }}license/license-manager.html#initlicense) multiple times in the same process. For example, if you call `initLicense` in both the `AppDelegate` and the `ViewController`, a conflict might occur.

✅ **Recommendation**: Call `initLicense` only once, ideally in the `AppDelegate`.

---

## Android: How do I import settings from the Barcode Scanner X app into my own app?

In the **Barcode Scanner X** app:

1. Navigate to the use case scenario of interest.
2. Tap **"Export Template"** at the bottom-right corner.

Once you have the template file, you can use it in your app with either:

- [`initSettings`]({{ site.dcvb_android_api }}capture-vision-router/settings.html)
- [`initSettingsFromFile`]({{ site.dcvb_android_api }}capture-vision-router/settings.html)


---