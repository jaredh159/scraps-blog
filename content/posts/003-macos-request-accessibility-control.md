---
title: 'Request Accessibility Control for a MacOS App'
date: 2021-04-23T16:18:58-04:00
slug: macos-request-accessibility-control
categories:
  - Swift
  - MacOS
---

If you need your app to have access to global events (like keystrokes) which require that
the app is granted authorization to _control your computer_ in the _Security and Privacy_
pane of system extensions, you can prompt the user for this privilege with the below code:

<!--more-->

```swift
let prompt = kAXTrustedCheckOptionPrompt.takeUnretainedValue() as String
let options: NSDictionary = [prompt: true]
let appHasPermission = AXIsProcessTrustedWithOptions(options)
if appHasPermission {
  // do something with permission, like `NSEvent.addGlobalMonitorForEvents()`
}
```
