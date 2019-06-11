---
layout: default
title: Home
nav_order: 1
summary: GeckoView, a webview from Mozilla specifically designed for Android browsers.
tags: [GeckoView,Gecko,mozilla,android,WebView,mobile,mozilla-central]
---

# Welcome to GeckoView

While Android offers a built-in WebView, it's not intended for building browsers, and many advanced Web APIs are disabled. Android's WebView is also a moving target: it's impossible know exactly which engine (and what version of that engine) will power a WebView on client devices.

In contrast, GeckoView is:

- **Full-Featured**: GeckoView is designed to expose the entire power of the Web to applications, including being suitable for building web browsers.
- **Self-Contained**: Because GeckoView is a standalone library that you bundle with your application, you can be confident that the code you test is the code that will actually run.
- **Standards Compliant**: Like Firefox, GeckoView offers excellent support for modern Web standards.

## Using GeckoView

* [Quick Start Guide][1]
* [Usage Documentation][7]

## API Documentation

* [Changelog][2]
* [API][3]

## More information
* [GeckoView Wiki][4]
* [GeckoView Source Code][5]
* [Raise a bug on GeckoView code][8]
* [Raise a documentation bug][6]

[1]:consumer/docs/geckoview-quick-start
[2]:javadoc/mozilla-central/org/mozilla/geckoview/doc-files/CHANGELOG
[3]:javadoc/mozilla-central/index.html
[4]:https://wiki.mozilla.org/Mobile/GeckoView
[5]:https://searchfox.org/mozilla-central/source/mobile/android/geckoview
[6]:https://github.com/mozilla/geckoview/issues
[7]:consumer/docs/index
[8]: https://bugzilla.mozilla.org/enter_bug.cgi?product=GeckoView
