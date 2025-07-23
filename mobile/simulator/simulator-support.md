---
layout: default-layout
title: Simulator Support - DBR Mobile FAQs
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, Android, iOS, simulator, camera, support
description: Does Dynamsoft Barcode Reader support simulator devices on Android and iOS?
needAutoGenerateSidebar: true
---

# Does Dynamsoft Barcode Reader support simulator devices?

[<< Back to FAQ index](index.md)

Yes, **Dynamsoft Barcode Reader (DBR)** supports simulator devices on both **Android** and **iOS**, but **only in limited scenarios**.

---

## ✅ When Simulator Support Works

If your app is only working with **static images** (e.g., from the photo library) and there is **no use of the camera**, then DBR will function properly on simulator devices.

---

## ❌ When Simulator Support Fails

If your app requires **interactive video scanning**, you will likely encounter errors due to the simulator's lack of physical camera access.

- On **Android**, attempting to open the camera using the [`open`](https://www.dynamsoft.com/camera-enhancer/docs/mobile/programming/android/primary-api/camera-enhancer.html#open) method in the **Camera Enhancer** will fail.
  
- On **iOS**, similar behavior occurs: calling [`open`](https://www.dynamsoft.com/camera-enhancer/docs/mobile/programming/ios/primary-api/camera-enhancer.html#open) may cause UI unresponsiveness or crashes, as **Camera Enhancer (DCE)** cannot function without actual hardware access.

---

## 💡 Tip for Mac M1/M2 Users (iOS Only)

If you're using a Mac with Apple Silicon (e.g., M1 or newer), you can test iOS apps on your **Mac directly** using Xcode:

1. In Xcode, select the **"My Mac (designed for iPhone/iPad)"** option as your target device.
2. This allows limited but effective testing of DBR on a macOS environment without a physical iOS device.

---

For full functionality, especially camera-based scanning, we recommend using **real devices** for both Android and iOS during development and testing.