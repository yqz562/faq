---
layout: default-layout
title: Reduce Battery Consumption - DBR iOS FAQs.
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, ios, battery, consumption
description: How can I reduce battery consumption? - DBR iOS FAQs.
needAutoGenerateSidebar: true
---

# How can I reduce battery consumption?

[<< Back to FAQ index](index.md)

If you are finding that the battery of your phone is being heavily consumed when using the Barcode Reader, there are a couple of things that you can do to potentially reduce the battery consumption, depending on the usage situation.

For a non-continuous video scanning scenario, make sure to call the [stopCapturing]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html#stopcapturing) method when the video scanning is no longer required.

For a continuous video scanning scenario, configure the [minImageCaptureInterval]({{ site.dcvb_ios_api }}capture-vision-router/auxiliary-classes/simplified-capture-vision-settings.html) attribute of `DSSimplifiedCaptureVisionSettings` class to set a higher value for the interval in order to reduce the frequency of fetching frames, thus reducing the number of scans per unit time, and thus, less resources needing to be consumed. You can dynamically adjust `minImageCaptureInterval` as needed to achieve the performance you are looking for.
