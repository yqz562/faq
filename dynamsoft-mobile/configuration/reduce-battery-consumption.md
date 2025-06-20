---
layout: default-layout
title: Reduce battery consumption - DBR Mobile FAQs
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, Android, iOS, battery, consumption
description: Learn how to reduce battery consumption in Android and iOS apps using Dynamsoft Barcode Reader.
needAutoGenerateSidebar: true
---

# How can I reduce battery consumption?

[<< Back to FAQ index](index.md)

If you're noticing high battery consumption while using Dynamsoft Barcode Reader (DBR) in your mobile application, there are several ways to optimize power usage based on your scanning scenario. The following tips apply to both Android and iOS unless otherwise noted.

---

## 🔋 General Recommendations

### Non-continuous video scanning

If scanning is only needed occasionally, be sure to stop the camera and barcode processing once the task is complete.  
Call the appropriate method to stop capturing:

- **Android**: [`stopCapturing`]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html#stopcapturing)  
- **iOS**: [`stopCapturing`]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html#stopcapturing)

This ensures that system resources like the camera and CPU are properly released, reducing battery drain.

---

### Continuous video scanning

In continuous scanning mode, you can reduce the scanning frequency to conserve energy. Both Android and iOS SDKs provide a setting for this:

- **Property**: `minImageCaptureInterval`  
- **Class**:
  - Android: [`SimplifiedCaptureVisionSettings`]({{ site.dcvb_android_api }}capture-vision-router/auxiliary-classes/simplified-capture-vision-settings.html)  
  - iOS: [`DSSimplifiedCaptureVisionSettings`]({{ site.dcvb_ios_api }}capture-vision-router/auxiliary-classes/simplified-capture-vision-settings.html)

Setting a **higher interval** reduces how often frames are fetched and processed, leading to:

- Fewer scans per second  
- Lower CPU/GPU usage  
- Extended battery life

This interval can be adjusted dynamically at runtime to strike the right balance between performance and power efficiency.

---