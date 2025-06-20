---
layout: default-layout
title: FAQ - Dynamsoft Barcode Reader iOS Edition
keywords: faq, mobile, ios
description: Dynamsoft Barcode Reader FAQ - Mobile (iOS)
needAutoGenerateSidebar: true
needGenerateH3Content: false
noTitleIndex: false
---

# FAQ - Mobile (iOS)

## What are the minimum system requirements of Dynamsoft Barcode Reader iOS?

- Supported OS: **iOS 11** or higher (**iOS 13** and higher recommended).
- Supported ABI: **arm64** and **x86_64**.
- Development Environment: Xcode 13 and above (Xcode 14.1+ recommended).

## How can I use AVCaptureSession or third-party camera modules with Dynamsoft Barcode Reader?

### AVCaptureSession

If you are using the CameraX, you can view [HelloWorld/DecodeWithAVCaptureSession sample](https://github.com/Dynamsoft/barcode-reader-mobile-samples/tree/main/ios/FoundationalAPISamples/DecodeWithAVCaptureSession) for a quick start.

### Third-Party Camera Module

If you are using a third-party camera module, what you have to do is:

- Create a class that extends [DSImageSourceAdapter]({{ site.dcvb_ios_api }}core/basic-structures/image-source-adapter.html). In this class, you need to implement the video capture features and the [`getImage`]({{ site.dcvb_ios_api }}core/basic-structures/image-source-adapter.html#getimage) method of [`DSImageSourceAdapter`]({{ site.dcvb_ios_api }}core/basic-structures/image-source-adapter.html).
- Create an instance of your camera class.
- Create an instance of the [`DSCaptureVisionRouter`]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html) class. Then trigger the [`setInput`]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html#setinput) method with the instance of your camera class as the parameter.
- Trigger the [`startCapturing`]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html#startcapturing) method to start the barcode decoding.

## Does Dynamsoft Barcode Reader iOS support simulator devices?

Yes, Dynamsoft Barcode Reader iOS can support simulator devices, but in a very limited capacity. If you are only working with existing images in the device's photo library, and there is **no use of the camera whatsoever**, then DBR iOS can work just fine on a simulator.

If you are attempting to test the SDK in an interactive video scenario, you will most likely encounter a UI unresponsiveness error that is caused by the camera open command in the code. More specifically, when the Camera Enhancer object call for the camera to open using the [open](https://www.dynamsoft.com/camera-enhancer/docs/mobile/programming/ios/primary-api/camera-enhancer.html#open) method.

If you have a Mac M1 machine (or a later model) then you can test your application on the Mac M1 machine directly via Xcode. In order to do that, please select _My Mac (designed for iPhone/iPad)_ in the dropdown menu when selecting the target device.

## Why does the page sometimes freeze when I start the scanner?

Before a barcode reader instance can be created, a one-time connection for license validation needs to occur when the app initializes (or whenever the license is set before the barcode reader instance creation). Sometimes, this license validation could take a second to complete.

A potential "freeze" of the page can occur if [`LicenseManager.initLicense()`]({{ site.dcvb_ios_api }}license/license-manager.html#initlicense) is called multiple times in a single process. For example, we have seen some Swift users call `initLicense` both in the ViewController file as well as AppDelegate. We recommend doing it in the AppDelegate file, and as long at it is not called in both files, then the implementation should be fine.

Please make sure that `initLicense` is called only once in your code.

## How can I reduce battery consumption?

If you are finding that the battery of your phone is being heavily consumed when using the Barcode Reader, there are a couple of things that you can do to potentially reduce the battery consumption, depending on the usage situation.

For a non-continuous video scanning scenario, make sure to call the [stopCapturing]({{ site.dcvb_ios_api }}capture-vision-router/multiple-file-processing.html#stopcapturing) method when the video scanning is no longer required.

For a continuous video scanning scenario, configure the [minImageCaptureInterval]({{ site.dcvb_ios_api }}capture-vision-router/auxiliary-classes/simplified-capture-vision-settings.html) attribute of `DSSimplifiedCaptureVisionSettings` class to set a higher value for the interval in order to reduce the frequency of fetching frames, thus reducing the number of scans per unit time, and thus, less resources needing to be consumed. You can dynamically adjust `minImageCaptureInterval` as needed to achieve the performance you are looking for.

## How can I implement continuous barcode scanning and one-off barcode scanning?

If you `startCapturing` successfully, the program will continuously decode the the video frames from the camera. As a result, you can continuously receive the barcode decoding results.

However, if you want to stop the barcode decoding thread, you can call the `stopCapturing` method when a barcode decoding result is received:

<div class="sample-code-prefix"></div>
>- Objective-C
>- Swift
>
>1. 
```objc
- (void)onDecodedBarcodesReceived:(DSDecodedBarcodesResult *)result {
   if (result.items.count > 0) {
          dispatch_async(dispatch_get_main_queue(), ^{
             [self.cvr stopCapturing];
          });
   }
}
```
2. 
```swift
func onDecodedBarcodesReceived(_ result: DecodedBarcodesResult) {
   if let items = result.items, items.count > 0 {
          DispatchQueue.main.async {
             self.cvr.stopCapturing()
          }
   }
}
```

## How to resolve the "Building for iOS Simulator, but linking in dylib built for iOS" error when building for the iOS simulator?](arm64-simulator-error.md)

DBR iOS can be used to build apps that belong to the arm64 architecture. If you try building an app for the arm64 simulator, and you migrated your app from an older version of Xcode to Xcode 12 or higher, then you might encounter the following error message:

> ld: "Building for iOS Simulator, but linking in dylib built for iOS, file '/ios/Pods/DynamsoftBarcodeReader/DynamsoftBarcodeReader.framework/DynamsoftBarcodeReader' for architecture arm64"

In order to fix the error, please take the following steps under the _Build Settings_ of the Xcode project:

1. Under _User-Defined_ -> find _VALIDATE_WORKSPACE_ and set it to **YES**. Rebuild your project.

2. Under _Architectures_ -> find _Build Active Architecture Only_ and set it to **YES**.

3. Under _Architectures_ -> make sure that _Architectures_ is set to $(ARCHS_STANDARD).

If the error message persists, please make one of the following changes:

- Instead of using the .framework (which all the samples do by default), switch to using the corresponding .xcframework

- Under the _Build Settings_ -> find _Excluded Architectures_ -> in the _Debug_ field click the + icon -> select _Any iOS Simulator SDK_ -> put "arm64"

- You can also exclude architectures via the Podfile as such:

  ```ruby
  post_install do |installer|
      installer.pods_project.build_configurations.each do |config|
          config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] = "arm64"
      end
  end
  ```

  OR

  ```ruby
  post_install do |installer|
      installer.pods_project.build_configurations.each do |config|
          config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] = "uname -m"
      end
  end
  ```

  OR

  ```ruby
  podspec:
  s.pod_target_xcconfig = { 'EXCLUDED_ARCHS[sdk=iphonesimulator*]' => 'arm64' }
  s.user_target_xcconfig = { 'EXCLUDED_ARCHS[sdk=iphonesimulator*]' => 'arm64' }
  ```

## How can I solve the "Undefined symbols for architecture armv7" error when building on iOS?

DBR iOS is compatible with the arm64 and x86_64 architectures only. If you attempt to build an app that is targetting the armv7 architecture, you will be met with an error from the Barcode Reader framework saying

> Undefined symbols for architecture armv7

Please note that this will mostly occur with older versions of Xcode or iOS that are still compatible with the older iOS device models that used the armv7 architecture. For most devices that are able to run iOS 11 and higher, the architecture will be arm64.

By default, when you set the _Architectures_ in _Build Settings_ to the "$(ARCHS_STANDARD) - Standard Architectures (arm64)", the armv7 architecture should automaticallt not be included. To ensure that your app ignores the armv7 architecture, you can add it to the _Excluded Architectures_ field of the _Build Settings_.

## How to import the settings of Barcode Scanner X app into my app?

In the Barcode Scanner X app, please go to the use case scenario that you are interested. On the right-bottom, tap on "Export Template".

Once you get the templates, you can implement them using the [`initSettings`]({{ site.dcvb_ios_api }}capture-vision-router/settings.html) or [`initSettingsFromFile`]({{ site.dcvb_ios_api }}capture-vision-router/settings.html) methods, depending on which input method you prefer.

> Note: The barcode scanner X is still using DBR v9.6.20 algorithm. You have to convert the exported template into v10.x before initializing it. [Download the converter](https://download2.dynamsoft.com/dcv/TemplateConverter.zip){:target="\_blank"}.

## How can I troubleshoot an image that fails to decode?

If the barcode is not recognized by Dynamsoft Barcode Reader, please do not hesitate to contact <a href="https://www.dynamsoft.com/contact/?ver=latest" target="_blank">Dynamsoft support team</a>.

Alternatively, here is the general troubleshooting steps:

1. Please ensure the lighting is not very bright or very dim.
2. Please ensure the aiming barcode format has been checked on.(Advanced Scan -> settings -> Barcode Format -> check the barcode formats)
3. We can decrease the Confidence level to increase the read rate.(Advanced Scan -> settings -> Result Settings -> Set Confidence Level to 10)
4. We can increase the deblur level to increase the read rate.(Advanced Scan -> settings -> Additional Settings -> increase DeblurLevel)

## Can I extract the driver’s information from a PDF417 barcode?

View the [DriversLicenseScanner sample](https://github.com/Dynamsoft/capture-vision-mobile-samples/tree/dcv_v2.6.1003/ios/DriversLicenseScanner){:target="\_blank"} for how to decode the PDF417 barcode on the driver's license and parse the driver's information.

> Note: Parsing the driver's information is an additional feature that requires a [DCV license](https://www.dynamsoft.com/customer/license/trialLicense/?product=cvs&utm_source=github&package=mobile){:target="\_blank"}.

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

## How to Enable QR Code Model 1 in BarcodeScannerX?

Nowadays, most QR codes are QR code Model 2. BarcodeScannerX, by default, only support QR code Model 2. If you want to test QR code Model 1 on BarcodeScannerX, here is what you can do:

1. Visit Dynamsoft barcode reader <a href="https://demo.dynamsoft.com/barcode-reader/" target="_blank">online demo</a>.
2. Click on Advanced Settings

   <div align="left">
      <p><img src="../assets/advanced-settings.jpg" width="40%" alt="advanced settings"></p>
   </div>

3. Check **EnableQRCodeModel1**(You can modify any other settings as you like)
4. Save the template.

   <div align="left">
      <p><img src="../assets/save-template.jpg" width="40%" alt="save template"></p>
   </div>

5. Send the template to <a href="https://www.dynamsoft.com/contact/?ver=latest" target="_blank">Dynamsoft support team</a>.
6. We will generate and send a link to you.
7. Click **Import Template** in the Advanced Scan settings of BarcodeScannerX. Then input the link.
8. Now you can scan QR code Model 1!

## How to Handle Non-printable Characters Like "\u{1D}" or "{GS}" from the Barcode Text?]({{site.faq_general}}unprintable-character.html?lang=objc,swift)

This page helps to you modify the barcode results when non-printable characters exists in the barcode text you decoded.

You always get 2 values that stands for the barcode decoding result from the `BarcodeResultItem` object:

- `barcodeBytes`
- `barcodeText`

Since `barcodeText` is a string value that generated from the `barcodeBytes`, is might be decoded into different characters based on different character encoding formats. When there exists a non-printable ASCII value (0 ~ 31 or 127) in the `barcodeBytes` array, the value is decoded into a messy code. Currently, the library doesn't provide methods to remove the non-printable characters nor convert them into printable characters, you have to add your own code to recognize the non-printable characters and replace or remove them. The following code snippet is an example for how to create a method for processing the `barcodeBytes` into a string you want.

**Code Snippet**

<div class="sample-code-prefix template2"></div>
   >- Objective-C
   >- Swift
   >
>
```objc
typedef NS_ENUM(NSInteger,EnumResultProcessMode)
{
    RPM_KEEP = 0,
    RPM_CONVERT = 1,
    RPM_REMOVE = 2
};
...
- (void)onDecodedBarcodesReceived:(DSDecodedBarcodesResult *)result {
    if (result.items.count > 0) {
        for (DSBarcodeResultItem *item in result.items) {
            NSString *modifiedBarcodeText = [self processResult:item.bytes mode:RPM_CONVERT isBreaklineKept:NO];
            msgText = [msgText stringByAppendingString:[NSString stringWithFormat:@"\nFormat: %@\nText: %@\n", item.formatString, modifiedBarcodeText]];
        }
    }
}
- (NSString *)processBarcodeBytes:(NSData *)byte
                     mode:(EnumResultProcessMode)mode
          isBreaklineKept:(BOOL)isKept{
    NSArray<NSNumber*>* _nonPrintingAsciiCharsKey = @[@0,@1,@2,@3,@4,@5,@6,@7,@8,@9,@10,@11,@12,@13,@14,@15,@16,@17,@18,@19,@20,@21,@22,@23,@24,@25,@26,@27,@28,@29,@30,@31,@127];
    NSArray<NSString*>* _nonPrintingAsciiCharsString = @[@"{NUL}",@"{SOH}",@"{STX}",@"{ETX}",@"{EOT}",@"{ENQ}",@"{ACK}",@"{BEL}",@"{BS}",@"{HT}",@"{LF}",@"{VT}",@"{FF}",@"{CR}",@"{SO}",@"{SI}",@"{DLE}",@"{DC1}",@"{DC2}",@"{DC3}",@"{DC4}",@"{NAK}",@"{SYN}",@"{ETB}",@"{CAN}",@"{EM}",@"{SUB}",@"{ESC}",@"{FS}",@"{GS}",@"{RS}",@"{US}",@"{DEL}"];
    NSMapTable<NSNumber*,NSString *> * _charValueToStringDict = [NSMapTable strongToStrongObjectsMapTable];
    for (int i=0; i<_nonPrintingAsciiCharsKey.count;i++){
        [_charValueToStringDict setObject:_nonPrintingAsciiCharsString[i] forKey:_nonPrintingAsciiCharsKey[i]];
    }
    const char* _Nonnull barcodeByteChar = byte.bytes;
    NSString *processedText = @"";
    for (int i=0;i<byte.length;i++){
        if ((isKept && (barcodeByteChar[i]==10 || barcodeByteChar[i]==13)) || mode==RPM_KEEP || ((int)barcodeByteChar[i]>31 && (int)barcodeByteChar[i]!=127 && (int)barcodeByteChar[i]!=0)){
            NSString *nextString = [NSString stringWithFormat:@"%c",barcodeByteChar[i]];
            processedText = [processedText stringByAppendingString:nextString];
        }
        else if (mode == RPM_CONVERT){
            NSNumber *keyValue = [[NSNumber alloc] initWithInt:(int)barcodeByteChar[i]];
            NSString *nextString = [_charValueToStringDict objectForKey:@2];
            processedText = [processedText stringByAppendingString:nextString];
        }
    }
    return processedText;
}
```
>
```swift
enum EnumResultProcessMode{
    case keep
    case convert
    case remove
}
func onDecodedBarcodesReceived(_ result: DecodedBarcodesResult) {
    if let items = result.items, items.count > 0 {
        for item in items {
            let processedBarcodeText = processBarcodeBytes(byte: item.bytes, processMode: EnumResultProcessMode.convert, isKeep: true)
            item.barcodeText = processedBarcodeText
        }
    }
}
private func processBarcodeBytes(byte:Data, processMode:EnumResultProcessMode, isKeep:Bool) -> String{
    let charValueToStringDict:NSDictionary = [0:"{NUL}",1:"{SOH}",2:"{STX}",3:"{ETX}",4:"{EOT}",5:"{ENQ}",6:"{ACK}",7:"{BEL}",8:"{BS}",9:"{HT}",10:"{LF}",11:"{VT}",12:"{FF}",13:"{CR}",14:"{SO}",15:"{SI}",16:"{DLE}",17:"{DC1}",18:"{DC2}",19:"{DC3}",20:"{DC4}",21:"{NAK}",22:"{SYN}",23:"{ETB}",24:"{CAN}",25:"{EM}",26:"{SUB}",27:"{ESC}",28:"{FS}",29:"{GS}",30:"{RS}",31:"{US}",127:"{DEL}"]
    var processedString = ""
    for i in 0...byte.count-1{
        if ((isKeep && ((byte[i]==10) || (byte[i]==13))) || (processMode == EnumResultProcessMode.keep) || ((byte[i]>31) && (byte[i] != 127) && (byte[i] != 0))){
            let nextText:String = String(bytes: [byte[i]], encoding: String.Encoding.utf8)!
            processedString += nextText as String
        }
        else if (processMode == EnumResultProcessMode.convert){
            let nextText:NSString = charValueToStringDict.object(forKey: byte[i]) as! NSString
            processedString += nextText as String
        }
    }
    return processedString
}
```
