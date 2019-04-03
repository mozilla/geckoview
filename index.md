---
layout: default
title: Home
nav_order: 1
summary: GeckoView, a webview from Mozilla specifically designed for Android browsers.
tags: [GeckoView,Gecko,mozilla,android,WebView,mobile,mozilla-central]
---

While Android offers a built-in WebView, it's not intended for building browsers, and many advanced Web APIs are disabled. Android's WebView is also a moving target: it's impossible know exactly which engine (and what version of that engine) will power a WebView on client devices.

In contrast, GeckoView is:

- **Full-Featured**: GeckoView is designed to expose the entire power of the Web to applications, including being suitable for building web browsers.
- **Self-Contained**: Because GeckoView is a standalone library that you bundle with your application, you can be confident that the code you test is the code that will actually run.
- **Standards Compliant**: Like Firefox, GeckoView offers excellent support for modern Web standards.

## Get Started with GeckoView

* [GeckoView Quick Start Guide][1]


## API Documentation

* [Changelog][2]
* [API](javadoc/mozilla-central/index.html)

## Get Started as a Contributor

* [GeckoView Contributor Quick Start Guide][3]
* [Mozilla Central Quick Start Guide][4]
* [Mozilla Central Contributor Guide][5]
* [Guide to Configuring GeckoView for Automation][6]
* [Guide to Native Debugging in Android Studio][7]


## More information
You can read more about GeckoView on the [wiki](https://wiki.mozilla.org/Mobile/GeckoView).

[1]:docs/geckoview-quick-start
[2]:javadoc/mozilla-central/org/mozilla/geckoview/doc-files/CHANGELOG
[3]:tutorials/geckoview-quick-start
[4]:tutorials/mc-quick-start
[5]:tutorials/contributing-to-mc
[6]:tutorials/automation
[7]:tutorials/native-debugging
