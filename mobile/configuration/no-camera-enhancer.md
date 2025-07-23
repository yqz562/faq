---
layout: default-layout
title: Use AVCaptureSession, CameraX or third-party camera modules - DBR Mobile FAQs.
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, android, ios, requirements
description: How can I use AVCaptureSession, CameraX or third-party camera modules with Dynamsoft Barcode Reader? - DBR Android FAQs.
needAutoGenerateSidebar: true
---

# How can I use AVCaptureSession, CameraX or third-party camera modules with Dynamsoft Barcode Reader - Android?

[<< Back to FAQ index](index.md)

# Android

## CameraX

If you are using the CameraX, you can view [HelloWorld/DecodeWithCamerX sample](https://github.com/Dynamsoft/barcode-reader-mobile-samples/tree/main/android/FoundationalAPISamples/DecodeWithCameraX) for a quick start.

## Third-Party Camera Module

If you are using a third-party camera module, what you have to do is:

- Create a class that extends [ImageSourceAdapter]({{ site.dcvb_android_api }}core/basic-structures/image-source-adapter.html). In this class, you need to implement the video capture features and the [`getImage`]({{ site.dcvb_android_api }}core/basic-structures/image-source-adapter.html#getimage) method of [`ImageSourceAdapter`]({{ site.dcvb_android_api }}core/basic-structures/image-source-adapter.html).
- Create an instance of your camera class.
- Create an instance of the [`CaptureVisionRouter`]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html) class. Then trigger the [`setInput`]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html#setinput) method with the instance of your camera class as the parameter.
- Trigger the [`startCapturing`]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html#startcapturing) method to start the barcode decoding.

# iOS

## AVCaptureSession

If you are using the CameraX, you can view [HelloWorld/DecodeWithAVCaptureSession sample](https://github.com/Dynamsoft/barcode-reader-mobile-samples/tree/v10.4.2002/ios/HelloWorld) for a quick start.

## Third-Party Camera Module

If you are using a third-party camera module, what you have to do is:

- Create a class that extends [DSImageSourceAdapter]({{ site.dcvb_ios_api }}core/basic-structures/image-source-adapter.html). In this class, you need to implement the video capture features and the [`getImage`]({{ site.dcvb_ios_api }}core/basic-structures/image-source-adapter.html#getimage) method of [`DSImageSourceAdapter`]({{ site.dcvb_ios_api }}core/basic-structures/image-source-adapter.html).
- Create an instance of your camera class.
- Create an instance of the [`DSCaptureVisionRouter`]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html) class. Then trigger the [`setInput`]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html#setinput) method with the instance of your camera class as the parameter.
- Trigger the [`startCapturing`]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html#startcapturing) method to start the barcode decoding.
