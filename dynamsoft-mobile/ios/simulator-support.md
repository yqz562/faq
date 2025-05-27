---
layout: default-layout
title: iOS Simulator Support - DBR iOS FAQs.
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, ios, simulator, camera
description: Does Dynamsoft Barcode Reader iOS Support Simulator Devices? - DBR iOS FAQs.
needAutoGenerateSidebar: true
---

# Does Dynamsoft Barcode Reader iOS support simulator devices?

[<< Back to FAQ index](index.md)

Yes, Dynamsoft Barcode Reader iOS can support simulator devices, but in a very limited capacity. If you are only working with existing images in the device's photo library, and there is **no use of the camera whatsoever**, then DBR iOS can work just fine on a simulator.

If you are attempting to test the SDK in an interactive video scenario, you will most likely encounter a UI unresponsiveness error that is caused by the camera open command in the code. More specifically, when the Camera Enhancer object call for the camera to open using the [open](https://www.dynamsoft.com/camera-enhancer/docs/mobile/programming/ios/primary-api/camera-enhancer.html#open) method.

Please note that DCE is currently not compatible with the simulator as the required use of a camera cannot be satisfied via the simulator.

However, if you have a Mac M1 machine (or a later model) then you can test your application on the Mac M1 machine directly via Xcode. In order to do that, please select *My Mac (designed for iPhone/iPad)* in the dropdown menu when selecting the target device.