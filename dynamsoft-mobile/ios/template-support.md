---
layout: default-layout
title: Extract Templates - DBR iOS FAQs.
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, ios, template, driver license, settings
description: How to import the settings of Barcode Scanner X app into my app? - DBR iOS FAQs.
needAutoGenerateSidebar: true
---

# How to import the settings of Barcode Scanner X app into my app?

[<< Back to FAQ index](index.md)

In the Barcode Scanner X app, please go to the use case scenario that you are interested. On the right-bottom, tap on "Export Template". 

Once you get the templates, you can implement them using the [`initSettings`]({{ site.dcvb_ios_api }}capture-vision-router/settings.html) or [`initSettingsFromFile`]({{ site.dcvb_ios_api }}capture-vision-router/settings.html) methods, depending on which input method you prefer.

> Note: The barcode scanner X is still using DBR v9.6.20 algorithm. You have to convert the exported template into v10.x before initializing it. [Download the converter](https://download2.dynamsoft.com/dcv/TemplateConverter.zip){:target="_blank"}.
