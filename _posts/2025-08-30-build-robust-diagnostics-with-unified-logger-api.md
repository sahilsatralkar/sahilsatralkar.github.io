---
layout: single
title: "Build Robust Diagnostics with the Unified Logger API"
date: 2025-08-30
categories: [iOS Development]
tags: [iOS, Swift, Logging, Debugging, Performance]
---

Apple's unified logging system supplies every iOS developer with a production-grade telemetry pipeline that is **structured, privacy-aware, and fast**—far superior to print() or NSLog[1][2].

---

## 1. Subsystems, Categories & Levels

Route each message by **subsystem** (bundle ID) and **category** (logical area). Console on macOS Sonoma lets you live-filter by these fields[3]:

```swift
import os

extension Logger {
    private static let subsystem = Bundle.main.bundleIdentifier!

    static let ui      = Logger(subsystem: subsystem, category: "ui")
    static let network = Logger(subsystem: subsystem, category: "network")
}
```

`Logger` exposes five levels—`trace`, `debug`, `info`, `error`, `fault`[4].

- `debug` for verbose flow during development
- `info` for high-level checkpoints
- `fault` for unrecoverable issues surfaced in crash reports[5]

Low-priority messages are discarded first in release builds, so binaries stay lean[1].

---

## 2. Privacy by Default

Every interpolated value is **private** unless you mark it .public[1]:

```swift
Logger.ui.debug("Selected item \(id, privacy: .public)")
Logger.ui.info("Settings toggled: \(flag)")  // redacted outside your process
```

With legacy os_log you must annotate %{private}@ yourself, but Swift interpolation is clearer and type-safe.

---

## 3. SwiftUI Hooks That Matter

**Lifecycle** onAppear confirms a view reached the screen[6].  
**State** onChange(of:initial:) (iOS 17) emits old → new values immediately[7].  
**Gestures** Capture taps or drags without breakpoints:

```swift
Text("Welcome")
    .onAppear { 
        Logger.ui.notice("WelcomeView appeared") 
    }
    .onChange(of: count, initial: true) { old, new in
        Logger.ui.info("count changed \(old) → \(new)")
    }
    .onTapGesture {
        Logger.ui.debug("View tapped")
    }
    // For location tracking, use DragGesture
    .gesture(
        DragGesture(minimumDistance: 0)
            .onEnded { value in
                Logger.ui.debug("Touch at \(value.location)")
            }
    )
```

---

## 4. Network Transparency

A dedicated logger makes HTTP diagnostics trivial:

```swift
// MARK: - Network call
let start = Date()
let (data, response) = try await URLSession.shared.data(for: request)

// MARK: - Log summary
if let httpResponse = response as? HTTPURLResponse {
    Logger.network.info("""
        \(request.httpMethod ?? "GET") \
        \(request.url!.path, privacy: .public) \          // visible in shared logs
        status \(httpResponse.statusCode, privacy: .public) \ // likewise
        in \(-start.timeIntervalSinceNow, format: .fixed(precision: 2)) s \
        payload \(data.count, format: .byteCount)
        """)
}
```

Only the path, status, and size are public; headers or bodies stay redacted.

---

## 5. Measure Performance with Signpost Intervals

Use signpost intervals (via trace-style logging) that Console renders as timelines—ideal for micro-benchmarks:

```swift
let signpostID = OSSignpostID(log: Logger.ui)
os_signpost(.begin, log: Logger.ui, name: "DatabaseSave", signpostID: signpostID)
// … critical section …
try context.save()
os_signpost(.end, log: Logger.ui, name: "DatabaseSave", signpostID: signpostID)
```

Watch the resulting interval in Console to spot regressions without opening Instruments.

---

## 6. Export a .logarchive for Remote Analysis

A **sysdiagnose** captures all unified logs plus system diagnostics:

1. Reproduce the issue on the device
2. Press **both volume buttons + side button** for ≈1 s, then release; a brief freeze/haptic confirms capture
3. Wait 1–2 min while iOS writes the archive to /private/var/tmp/
4. Retrieve the file:
   - Finder → iPhone → Files → Logs, or
   - Settings ▸ Privacy & Security ▸ Analytics Data (iOS 17)
5. Open the .logarchive in Console or Xcode Organizer, filter by subsystem/category, inspect levels, intervals, and redacted placeholders. Privacy flags remain intact[1]

Because the archive is self-contained, QA or testers can send it safely; you retain full context without shipping a debug build.

---

## 7. What Console Brings to the Table

Console is a built-in macOS application (found in /Applications/Utilities/) that serves as the primary viewer for Apple's unified logging system. It connects to iOS devices and simulators to display, filter, and analyze log messages in real-time.

Console is the Swiss-army knife for unified logs:

- **Live stream** device logs over USB or Wi-Fi
- **Instant filters** for device, process, subsystem, category, or level
- **Pinned predicates** for one-click access to common views (e.g., network errors)
- **Interval charts** for trace pairs, highlighting performance cliffs
- **Selective export** of log slices to share with colleagues

---

## 8. Common Pitfalls

1. **Logging every loop in debug**—audit and prune
2. **Forgetting .public**—values appear <private> when you need them most
3. **One global logger**—without categories, filtering is painful
4. **Marking warnings as fault**—pollutes crash workflows

---

## Apple Documentation References

- Unified logging overview – Apple Developer[1]
- Logger API – Apple Developer[2]
- log(level:_:) and trace usage[4]
- fault semantics in OSLogType[5]
- View logs in Console – Apple Support[3]
- onChange(of:initial:) in SwiftUI[7]
- onAppear(perform:) lifecycle hook[6]

---

## Takeaway

With thoughtful subsystems, level discipline, and SwiftUI hooks, Logger delivers searchable, lightweight, privacy-compliant diagnostics that scale from simulator runs to production crash reports—no third-party SDK required. Replace print() today; the platform already has your back.

## Sources

[1] [Logging | Apple Developer Documentation](https://developer.apple.com/documentation/os/logging)  
[2] [Logger | Apple Developer Documentation](https://developer.apple.com/documentation/os/logger)  
[3] [View log messages in Console on Mac](https://support.apple.com/en-in/guide/console/cnsl1012/mac)  
[4] [log(level:_:) | Apple Developer Documentation](https://developer.apple.com/documentation/os/logger/log(level:_:))  
[5] [fault(_:) | Apple Developer Documentation](https://developer.apple.com/documentation/os/logger/fault(_:))  
[6] [onAppear(perform:) | Apple Developer Documentation](https://developer.apple.com/documentation/swiftui/view/onappear(perform:))  
[7] [onChange(of:initial:_:) | Apple Developer Documentation](https://developer.apple.com/documentation/SwiftUI/View/onChange(of:initial:_:)-4psgg)