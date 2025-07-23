---
layout: default-layout
title: How to check the version of the JS SDK I am currently using?
keywords: Dynamsoft Barcode Reader, FAQ, tech basic, check version, current version
description: How to check the version of the JS SDK I am currently using?
needAutoGenerateSidebar: false
---

# How to check the version of the JS SDK I am currently using?

[<< Back to FAQ index](index.md)

There are multiple ways to check the version currently being used -

- The first way is to use the [version API](https://www.dynamsoft.com/barcode-reader/programming/javascript/api-reference/InitializationControl.html?ver=latest#version). Using this API in the browser console should print out the version of the library being used by the web app.
- If you are using the library via npm or yarn, then you can check the version of the package via

    ```bash
    npm –v dynamsoft-javascript-barcode
    ```

- If you are including the library via the CDN link, then the version number should be mentioned in that reference link.

<div class="sample-code-prefix template2"></div>
   >- Javascript
   >- Objective-C
   >- Swift
   >- Android
   >- Python
   >- C++
   >- C#
   >
>
```javascript
const version = Dynamsoft.DBR.BarcodeReaderModule.getVersion();
console.log(version);
```
>
```objc
NSString *version = [DSCaptureVisionRouterModule getVersion];
```
>
```swift
let version = CaptureVisionRouterModule.getVersion()
```
>
```java
BarcodeReaderModule reader = BarcodeReaderModule();
String versionInfo = reader.getVersion();
```
>
```python
reader = BarcodeReaderModule()
print(reader.get_version())
```
>
```c++
const char* version = CCaptureVisionRouterModule::GetVersion();
```
>
```csharp
using (CaptureVisionRouter cvr = new CaptureVisionRouter())
{
   SimplifiedCaptureVisionSettings settings;
   string errorMsg;
   // Obtain current runtime settings of `CCaptureVisionRouter` instance.
   cvr.GetSimplifiedSettings(PresetTemplate.PT_READ_BARCODES, out settings);
   // Specify the barcode formats by enumeration values.
   // Use "|" to enable multiple barcode formats at one time.
   settings.barcodeSettings.barcodeFormatIds = (ulong)(EnumBarcodeFormat.BF_QR_CODE | EnumBarcodeFormat.BF_ONED);
   // Update the settings.
   cvr.UpdateSettings(PresetTemplate.PT_READ_BARCODES, settings, out errorMsg);  
}
```
