---
layout: default-layout
title: Minimum System Requirements - DBR Mobile FAQs
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, Android, iOS, requirements
description: What are the minimum system requirements for Dynamsoft Barcode Reader on Android and iOS?
needAutoGenerateSidebar: true
---

# What are the minimum system requirements for Dynamsoft Barcode Reader?

[<< Back to FAQ index](index.md)

Dynamsoft Barcode Reader (DBR) supports a variety of Android and iOS environments. Please refer to the platform-specific tables below.

---

## Android Requirements

| **Component**                 | **Requirement**                             |
| ----------------------------- | ------------------------------------------- |
| **Supported OS**              | Android 5.0 (API Level 21) or higher        |
| **Supported ABI**             | `armeabi-v7a`, `arm64-v8a`, `x86`, `x86_64` |
| **Java Version**              | Java 8                                      |
| **Simulator Support**         | Yes                                         |
| **Unsupported Architectures** | None                                        |

---

## iOS Requirements

| **Component**                 | **Requirement**                                 |
| ----------------------------- | ----------------------------------------------- |
| **Supported OS**              | iOS 11 or higher<br>(iOS 13+ recommended)       |
| **Supported ABI**             | `arm64`, `x86_64` (for simulator use)           |
| **Development Environment**   | Xcode 13 and above<br>(Xcode 14.1+ recommended) |
| **Simulator Support**         | Yes — must use `.xcframework`                   |
| **Unsupported Architectures** | `armv7` (must be excluded in build settings)    |

> 💡 **Note for iOS**:
>
> - Use `.xcframework` when testing in the iOS Simulator.
> - Avoid building for `armv7` as it is not supported by DBR.

---
