---
layout: default
title: Home
nav_order: 1
---

While Android offers a built-in WebView, it's not intended for building browsers, and many advanced Web APIs are disabled. Android's WebView is also a moving target: it's impossible know exactly which engine (and what version of that engine) will power a WebView on client devices.

In contrast, GeckoView is:

- **Full-Featured**: GeckoView is designed to expose the entire power of the Web to applications, including being suitable for building web browsers.
- **Self-Contained**: Because GeckoView is a standalone library that you bundle with your application, you can be confident that the code you test is the code that will actually run.
- **Standards Compliant**: Like Firefox, GeckoView offers excellent support for modern Web standards.

{% include_relative README.md %}
