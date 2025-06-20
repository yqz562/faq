---
layout: default-layout
title: Export Templates - DBR Mobile FAQs
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, android, ios, template, driver license, settings
description: How to import the settings of Barcode Scanner X app into my app? - DBR Mobile FAQs.
needAutoGenerateSidebar: true
---

# How to import the settings of Barcode Scanner X app into my app?

[<< Back to FAQ index](index.md)

In the Barcode Scanner X app, navigate to the use case scenario you are interested in. Tap the **"Export Template"** button at the bottom right corner.

Once you obtain the templates, you can implement them using either of the following methods:

## iOS

- [`initSettings`]({{ site.dcvb_ios_api }}capture-vision-router/settings.html)
- [`initSettingsFromFile`]({{ site.dcvb_ios_api }}capture-vision-router/settings.html)

## Android

- [`initSettings`]({{ site.dcvb_android_api }}capture-vision-router/settings.html)
- [`initSettingsFromFile`]({{ site.dcvb_android_api }}capture-vision-router/settings.html)

> **Note:** Barcode Scanner X currently uses the **DBR v9.6.20** algorithm. You must convert the exported template to **v10.x** before initializing it in your app.  
> 👉 [Download the converter](https://download2.dynamsoft.com/dcv/TemplateConverter.zip){:target="\_blank"}.
