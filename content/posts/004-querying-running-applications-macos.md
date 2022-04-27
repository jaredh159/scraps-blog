---
title: 'Querying Running Applications in MacOS'
date: 2021-04-23T16:26:46-04:00
slug: 'querying-running-applications-in-macos'
categories:
  - Swift
  - MacOS
---

If you want to list out all of the currently running applications in a MacOS app, you can
do:

<!--more-->

```swift
for app in NSWorkspace.shared.runningApplications {
  print(app.localizedName!)
}
```

This will give you a whole bunch of running "applications", like:

```txt
loginwindow
ViewBridgeAuxiliary
talagent
Dock
ViewBridgeAuxiliary
QuickLookUIService (PID 363)
Finder
Wi-Fi
Notification Center
com.apple.dock.extra
Spotlight
Sync
AppSSOAgent
Alfred
TextInputMenuAgent
imklaunchagent
AirPlayUIAgent
... many more ...
```

If you're only interested in the normal user-apps that appear in the Dock, you would
filter on the `.activationPolicy` like so:

```swift
for app in NSWorkspace.shared.runningApplications {
  if app.activationPolicy == .regular {
    print(app.localizedName!)
  }
}
```

Producing a much smaller list:

```txt
Finder
Xcode
Things
iTerm2
Console
Brave Browser
Slack
Code
Simulator
Google Chrome
Safari
```

Finally, if your app is doing something in the background (like observing global events),
and you want to know what app is currently focused, or active (frontmost), you can get the
same with `NSWorkspace.shared.frontmostApplication?.localizedName`
