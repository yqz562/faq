---
layout: default-layout
title: Dynamsoft Barcode Reader FAQ - Mobile (Android)
keywords: faq, mobile, android
description: Dynamsoft Barcode Reader FAQ - Mobile (Android)
needAutoGenerateSidebar: true
needGenerateH3Content: false
noTitleIndex: false
---

# FAQ - Mobile (Android)

## What are the minimum system requirements of Dynamsoft Barcode Reader Android?

- Supported OS: Android 5.0 (API Level 21) or higher.
- Supported ABI: **armeabi-v7a**, **arm64-v8a**, **x86** and **x86_64**.
- Development Environment: Android Studio 2022.2.1 or higher.

## How can I use CameraX or third-party camera modules with Dynamsoft Barcode Reader?

### CameraX

If you are using the CameraX, you can view [DecodeWithCamerX sample](https://github.com/Dynamsoft/barcode-reader-mobile-samples/tree/main/android/FoundationalAPISamples/DecodeWithCameraX) for a quick start.

### Third-Party Camera Module

If you are using a third-party camera module, what you have to do is:

- Create a class that extends [ImageSourceAdapter]({{ site.dcvb_android_api }}core/basic-structures/image-source-adapter.html). In this class, you need to implement the video capture features and the [`getImage`]({{ site.dcvb_android_api }}core/basic-structures/image-source-adapter.html#getimage) method of [`ImageSourceAdapter`]({{ site.dcvb_android_api }}core/basic-structures/image-source-adapter.html).
- Create an instance of your camera class.
- Create an instance of the [`CaptureVisionRouter`]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html) class. Then trigger the [`setInput`]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html#setinput) method with the instance of your camera class as the parameter.
- Trigger the [`startCapturing`]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html#startcapturing) method to start the barcode decoding.

## Does Dynamsoft Barcode Reader Android support simulator devices?

Yes, DBR Android can support simulator devices, but in a very limited capacity. If you are only working with existing images in the device's photo library, and there is **no use of the camera whatsoever**, then DBR Android can work just fine on a simulator.

If you are attempting to test the SDK in an interactive video scenario, you will most likely encounter an error that is caused by the camera open command in the code. More specifically, when the Camera Enhancer object call for the camera to open using the [open](https://www.dynamsoft.com/camera-enhancer/docs/mobile/programming/android/primary-api/camera-enhancer.html#open) method.

Please note that DCE is not compatible with the simulator as the required use of a camera cannot be satisfied via the simulator.

## Why does the page sometimes freeze when I start the scanner?

Before a barcode reader instance can be created, a one-time connection for license validation needs to occur when the app initializes (or whenever the license is set before the barcode reader instance creation). Sometimes, this license validation could take a second to complete.

A potential "freeze" of the page can occur if `initLicense()` is called multiple times in a single process. Please make sure that `initLicense` is called only once in your code.

To help troubleshoot whether the method is being called multiple times, we recommend stepping through the code using a debugger.

## How can I implement continuous barcode scanning and one-off barcode scanning?

If you `startCapturing` successfully, the program will continuously decode the the video frames from the camera. As a result, you can continuously receive the barcode decoding results.

However, if you want to stop the barcode decoding thread, you can call the `stopCapturing` method when a barcode decoding result is received:

```java
mRouter.addResultReceiver(new CapturedResultReceiver() {
    @Override
    public void onDecodedBarcodesReceived(DecodedBarcodesResult result) {
        // mRouter is the instance of CaptureVisionRouter.
        mRouter.stopCapturing();
    }
});
```

## How can I reduce battery consumption?

If you are finding that the battery of your phone is being heavily consumed when using the Barcode Reader, there are a couple of things that you can do to potentially reduce the battery consumption, depending on the usage situation.

For a non-continuous video scanning scenario, make sure to call the [stopCapturing]({{ site.dcvb_android_api }}capture-vision-router/multiple-file-processing.html#stopcapturing) method when the video scanning is no longer required.

For a continuous video scanning scenario, configure the [minImageCaptureInterval]({{ site.dcvb_android_api }}capture-vision-router/auxiliary-classes/simplified-capture-vision-settings.html) attribute of `SimplifiedCaptureVisionSettings` class to set a higher value for the interval in order to reduce the frequency of fetching frames, thus reducing the number of scans per unit time, and thus, less resources needing to be consumed. You can dynamically adjust `minImageCaptureInterval` as needed to achieve the performance you are looking for.

## How to import the settings of Barcode Scanner X app into my app?

In the Barcode Scanner X app, please go to the use case scenario that you are interested. On the right-bottom, tap on "Export Template".

Once you get the templates, you can implement them using the [`initSettings`]({{ site.dcvb_android_api }}capture-vision-router/settings.html) or [`initSettingsFromFile`]({{ site.dcvb_android_api }}capture-vision-router/settings.html) methods, depending on which input method you prefer.

## How can I troubleshoot an image that fails to decode?

If the barcode is not recognized by Dynamsoft Barcode Reader, please do not hesitate to contact <a href="https://www.dynamsoft.com/contact/?ver=latest" target="_blank">Dynamsoft support team</a>.

Alternatively, here is the general troubleshooting steps:

1. Please ensure the lighting is not very bright or very dim.
2. Please ensure the aimming barcode format has been checked on.(Advanced Scan -> settings -> Barcode Format -> check the barcode formats)
3. We can decrease the Confidence level to increase the read rate.(Advanced Scan -> settings -> Result Settings -> Set Confidence Level to 10)
4. We can increase the deblur level to increase the read rate.(Advanced Scan -> settings -> Additional Settings -> increase DeblurLevel)

## Can I extract the driver’s information from a PDF417 barcode?

View the [DriversLicenseScanner sample](https://github.com/Dynamsoft/capture-vision-mobile-samples/tree/dcv_v2.6.1003/Android/DriversLicenseScanner){:target="\_blank"} for how to decode the PDF417 barcode on the driver's license and parse the driver's information.

> Note: Parsing the driver's information is an additional feature that requires a [DCV license](https://www.dynamsoft.com/customer/license/trialLicense/?product=cvs&utm_source=github&package=mobile){:target="\_blank"}.

## Can I reduce the size of the final Android app?

It is recommended that you distribute your app using App Bundle in order to reduce the final size of the Android app.

The second step is to utilize APK splits. To learn more about this, please refer to this [page](https://developer.android.com/studio/build/configure-apk-splits#configure-abi-split){:target="\_blank"}.

The third thing to do is to remove processor architecture support. If you won't be distributing your app via Google Play, please refer to this [page](https://developer.android.com/ndk/guides/abis#gc){:target="\_blank"} on how to proceed with this step.

## How to use Debug Mode in Barcode Scanner X?

If you are experiencing app crashes in your own application or you’ve come across some barcode(s) that you can’t read and you have exhausted all of the other troubleshooting methods, Debug Mode of the [BarcodeScannerX](https://www.dynamsoft.com/barcode-reader/sdk-mobile/#appDemo) demo app can help offer one last effort to resolve these issues.

This next section will explain how to toggle on debug mode on the demo app, and will then dive into how to collect crash logs and/or image samples.

1. From the home screen, go to Advanced Scan.

<img src="../assets/home_screen.jpg" alt="Home screen"  width="50%" height="50%">

2. Tap the settings icon at the top-right corner.

<img src="../assets/advanced_scan.jpg" alt="Advanced scan"  width="50%" height="50%">

3. Tap Debug Mode to see the drop-down list.

<img src="../assets/debug_mode.jpg" alt="Debug mode"  width="50%" height="50%">

### Debug Mode - Crash Logger

If you are encountering an app crash caused by Dynamsoft Barcode Reader or Dynamsoft Camera Enhancer SDK, you need to use the Crash Logger.

1. Toggle on Crash Logger

<img src="../assets/crash_toggle_on.jpg" alt="Crash toggle on"  width="50%" height="50%">

2. After Crash Logger is toggled on, please go ahead and scan codes until you reproduce the crash issue.

3. After the app crashes, re-open BarcodeScannerX app and go to Advanced Scan -> settings. Tap the "Share" button to share the log files with the [Dynamsoft support team](https://www.dynamsoft.com/contact/?ver=latest).

<img src="../assets/crash_share.jpg" alt="Crash share"  width="50%" height="50%">

### Debug Mode - Image Cropper

If you are having trouble reading barcodes, you should use the Image Cropper to capture some sample image(s) or frame(s) and send them to the Dynamsoft Support Team:

1. Toggle on Image Cropper

<img src="../assets/image_cropper_toggle.jpg" alt="Image crop toggle on"  width="50%" height="50%">

2. After Image Cropper is toggled on, an image crop icon will show up at the bottom left of Advanced Scan

<img src="../assets/crop.jpg" alt="crop"  width="50%" height="50%">

3. Tap the image crop icon to crop and share the original frames with the [Dynamsoft support team](https://www.dynamsoft.com/contact/?ver=latest). Our support team will investigate the video frames and get back to you with a solution as soon as possible.

## How to Enable QR Code Model 1 in Barcode Scanner X?

Nowadays, most QR codes are QR code Model 2. BarcodeScannerX, by default, only support QR code Model 2. If you want to test QR code Model 1 on BarcodeScannerX, here is what you can do:

1. Visit Dynamsoft barcode reader <a href="https://demo.dynamsoft.com/barcode-reader/" target="_blank">online demo</a>.
2. Click on Advanced Settings

   <div align="left">
      <p><img src="../assets/advanced-settings.jpg" width="40%" alt="advanced settings"></p>
   </div>

3. Check **EnableQRCodeModel1**.(You can modify any other settings as you like)
4. Save the template.

   <div align="left">
      <p><img src="../assets/save-template.jpg" width="40%" alt="save template"></p>
   </div>

5. Send the template to <a href="https://www.dynamsoft.com/contact/?ver=latest" target="_blank">Dynamsoft support team</a>.
6. We will generate and send a link to you.
7. Click **Import Template** in the Advanced Scan settings of BarcodeScannerX. Then input the link.
8. Now you can scan QR code Model 1!

## How to Handle Non-printable Characters Like "\u{1D}" or "{GS}" from the Barcode Text?

This page helps to you modify the barcode results when non-printable characters exists in the barcode text you decoded.

You always get 2 values that stands for the barcode decoding result from the `CBarcodeResultItem` object:

- `barcodeBytes`
- `barcodeText`

Since `barcodeText` is a string value that generated from the `barcodeBytes`, is might be decoded into different characters based on different character encoding formats. When there exists a non-printable ASCII value (0 ~ 31 or 127) in the `barcodeBytes` array, the value is decoded into a messy code. Currently, the library doesn't provide methods to remove the non-printable characters nor convert them into printable characters, you have to add your own code to recognize the non-printable characters and replace or remove them. The following code snippet is an example for how to create a method for processing the `barcodeBytes` into a string you want.

**Code Snippet**

```java
mRouter.addResultReceiver(new CapturedResultReceiver() {
    @Override
    // Implement the callback method to receive DecodedBarcodesResult.
    // The method returns a DecodedBarcodesResult object that contains an array of BarcodeResultItems.
    // BarcodeResultItems is the basic unit from which you can get the basic info of the barcode like the barcode text and barcode format.
    public void onDecodedBarcodesReceived(DecodedBarcodesResult result) {
        process = new ProcessBarcodeResultUtil();
        if (result!=null && result.getItems().length!=0){
            for (int i=0; i< result.getItems().length; i++){
                // The return value is the modified barcode text.
                String processedResult = process.processBarcodeByte(result.getItems().getBytes(),ProcessBarcodeResultUtil.ProcessNonPrintingCharsMode.PNPCM_REMOVE,true);
                Log.i("ProcessByte", "onDecodedBarcodesReceived: processedResult = "+processedResult);
            }
        }
    }
});
// Create a ProcessBarcodeResultUtil class
public class ProcessBarcodeResultUtil {
    enum ProcessNonPrintingCharsMode{
        PNPCM_KEEP,
        PNPCM_REMOVE,
        PNPCM_CONVERT
    }
    final HashMap<Integer, String> charValueToStringDict = new HashMap<Integer, String>();
    ProcessBarcodeResultUtil(){
        final int[] NonPrintingAsciiCharsValue = {0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,127};
        final String[] NonPrintingAsciiCharsString = {
                "{NUL}","{SOH}","{STX}","{ETX}","{EOT}","{ENQ}","{ACK}","{BEL}","{BS}","{HT}","{LF}","{VT}","{FF}","{CR}","{SO}","{SI}",
                "{DLE}","{DC1}","{DC2}","{DC3}","{DC4}","{NAK}","{SYN}","{ETB}","{CAN}","{EM}","{SUB}","{ESC}","{FS}","{GS}","{RS}","{US}","{DEL}"
        };
        for (int i = 0; i < 33; ++i){
            charValueToStringDict.put(NonPrintingAsciiCharsValue[i], NonPrintingAsciiCharsString[i]);
        }
    }
    public String processBarcodeByte(byte[] barcodeByte, ProcessNonPrintingCharsMode mode, boolean keepLineBreak){
        StringBuilder processedResult = new StringBuilder();
        for (int i=0; i<barcodeByte.length; i++){
            int byteValue = (int)barcodeByte[i];
            if ((!charValueToStringDict.containsKey(byteValue)) || ((byteValue == 10 || byteValue == 13) && keepLineBreak) || mode == ProcessNonPrintingCharsMode.PNPCM_KEEP){
                processedResult.append((char)barcodeByte[i]);
            }
            else if(mode == ProcessNonPrintingCharsMode.PNPCM_CONVERT){
                processedResult.append(charValueToStringDict.get(byteValue));
            }
        }
        return processedResult.toString();
    }
}
```
