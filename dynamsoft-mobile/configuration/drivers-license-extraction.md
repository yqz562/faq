---
layout: default-layout
title: Read Driver's License - DBR Mobile FAQs
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, Android, iOS, PDF417, driver license, decode, parser
description: Can I extract the driver’s information from a PDF417 barcode? - DBR Android & iOS FAQs.
needAutoGenerateSidebar: true
---

# Can I extract the driver’s information from a PDF417 barcode?

[<< Back to FAQ index](index.md)

Yes, you can extract driver’s license information from a PDF417 barcode using the **Dynamsoft Barcode Reader** in combination with the **Dynamsoft Code Parser**.

Check out the sample project on GitHub to see how to decode the PDF417 barcode and parse the data:

👉 [DriversLicenseScanner Sample (Android)](https://github.com/Dynamsoft/capture-vision-mobile-samples/tree/dcv_v2.6.1003/Android/DriversLicenseScanner){:target="\_blank"}  
👉 [DriversLicenseScanner Sample (iOS)](https://github.com/Dynamsoft/capture-vision-mobile-samples/tree/dcv_v2.6.1003/iOS/DriversLicenseScanner){:target="\_blank"}

> These samples include the `DynamsoftCodeParser` library, which is used to extract structured information (such as name, address, license number, etc.) from the raw barcode decoding result.
>
> A **valid license** is required to use the `DynamsoftCodeParser` library.

---
