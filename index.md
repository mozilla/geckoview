---
layout: default
title: Home
nav_order: 1
summary: GeckoView, a webview from Mozilla specifically designed for Android browsers.
tags: [GeckoView,Gecko,mozilla,android,WebView,mobile,mozilla-central]
---

Android offers a built-in WebView, which applications can hook into in order to display web pages within the context of their app. However, Android's WebView is not intended for building browsers, as many advanced Web APIs are disabled. Furthermore, it is also a moving target: it's impossible to know exactly which engine (and what version of that engine) will power a WebView on client devices. 

That is where GeckoView comes in. GeckoView is:

- **Full-Featured**: GeckoView is designed to expose the entire power of the Web to applications, and all that through a straightforward API.
- **Suited for apps and browsers**: GeckoView is particularly suited for building mobile browsers, but it can be embedded as a web engine component in any kind of app.
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
* [Guide to Native Debugging in Android Studio][6]


## More information
You can read more about GeckoView on the [wiki](https://wiki.mozilla.org/Mobile/GeckoView).

[1]:docs/geckoview-quick-start
[2]:javadoc/mozilla-central/org/mozilla/geckoview/doc-files/CHANGELOG
[3]:tutorials/geckoview-quick-start
[4]:tutorials/mc-quick-start
[5]:tutorials/contributing-to-mc
[6]:tutorials/native-debugging
