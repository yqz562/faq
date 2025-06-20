---
layout: default-layout
title: Why does it sometimes Freeze when I Enter the Scan Page? 
keywords: Dynamsoft Barcode Reader, FAQ, Mobile, tech basic, ios, freeze, page
description: Why does the page sometimes freeze when I start the scanner?
needAutoGenerateSidebar: true
---

# Why does the page sometimes freeze when I start the scanner?

[<< Back to FAQ index](index.md)

Before a barcode reader instance can be created, a one-time connection for license validation needs to occur when the app initializes (or whenever the license is set before the barcode reader instance creation). Sometimes, this license validation could take a second to complete.

A potential "freeze" of the page can occur if `BarcodeReader.initLicense()` is called multiple times in a single process. For example, we have seen some Swift users call `initLicense` both in the ViewController file as well as AppDelegate. We recommend doing it in the AppDelegate file, and as long at it is not called in both files, then the implementation should be fine. 

Please make sure that `initLicense` is called only once in your code.