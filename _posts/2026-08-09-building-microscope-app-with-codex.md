---
layout: single
title: "From Market Research to the App Store: Building Microscope App with the Codex App"
date: 2026-08-09
permalink: /blog/building-microscope-app-with-codex/
categories: [iOS Development, Indie Development, AI]
tags: [SwiftUI, AVFoundation, StoreKit 2, ASO, Codex, IndieAppKit, App Store]
header:
  teaser: /assets/images/microscope-app-01-hero.jpg
---

The idea for **Microscope App** began with market research in Astro. I was looking for an App Store category with enough demand to support organic discovery and a realistic level of competition.

Astro's US data showed favourable demand and competition for microscope-focused searches. Broader magnifier terms had more demand, but they were also more competitive and less specific to the product I would eventually build.

That evidence was favourable enough to continue investigating the niche. I registered the name **Microscope App** in App Store Connect, then moved into detailed competitor analysis.

The competitor analysis was documented on June 30, 2026. Just over five weeks later, on August 6, version 1.0 build 5 was available on the App Store.

Between those dates, the repository records competitor and keyword research, a product requirements document, onboarding specifications, the SwiftUI and AVFoundation implementation, automated and physical-device testing, eight localizations, App Store artwork, privacy and accessibility evidence, StoreKit configuration, TestFlight validation, and the final App Review handoff.

The Codex app was used during the build and verification work. It also ran tests against my connected physical iPhone 17, not only against Simulator fakes. The repository separately records Codex-assisted localization checks and the generated marketing compositions used for the App Store campaign.

This is the documented journey from Astro research and App Store name registration to version 1.0 on the App Store.

> Disclosure: The App Store marketing compositions shown in this article use generated representative hardware and specimen imagery. They demonstrate the product's intended viewing experience; they are not presented as scientific captures made by the app.

The live product and project are here:

- [Microscope App on the App Store](https://apps.apple.com/app/id6784896706)
- [Microscope App source repository](https://github.com/sahilsatralkar/Microscope-App)
- [Support and frequently asked questions](https://sahilsatralkar.com/apps/microscope/support)

<!-- Publishing asset source: screenshots/final/English/01-turn-your-microscope-into-a-camera.png -->
<img src="/assets/images/microscope-app-01-hero.jpg" alt="A physical microscope with an iPhone mounted over its eyepiece and Microscope App displaying a specimen" width="62%" style="display:block; margin:1.75rem auto 0.75rem; border-radius:18px;" />

*The launch hero communicates the essential requirement immediately: Microscope App works with a physical microscope and a compatible iPhone eyepiece adapter.*

## Astro identified the initial opportunity

Astro is an App Store Optimization research tool. It helps developers evaluate keyword demand and competition, track rankings, and examine the keywords and metadata used by competing apps.

I used Astro as the primary source for App Store keyword research, rankings, competitor results, and keyword extraction. Google Trends was limited to alerting for unusual demand changes, while competitor metadata and reviews were used to validate intent.

The distinction between broad demand and relevant demand mattered. Generic magnifier searches described a larger but less focused utility market. Microscope-specific searches matched the proposed product more closely and presented a more favourable opportunity for organic discovery.

The research therefore supported a specific organic-search direction rather than a generic camera or magnifier app. It also established **Microscope App** as the fixed product name before the detailed product work began.

## Competitor analysis tested the idea

The initial research covered six microscope, magnifier, and microscope-adjacent iPhone apps. I compared their App Store positioning, ratings, pricing, reviews, public download signals, feature sets, websites, and promotion strategies.

The category was more complicated than the word *microscope* suggested.

Some products were general magnifying-glass utilities. Some were companion apps for proprietary Wi-Fi microscope hardware. A smaller group supported the workflow I cared about: placing an iPhone over the eyepiece of an ordinary physical microscope and using its camera as a viewer and capture device.

User reviews exposed consistent problems:

- Focus was blurry or difficult to control.
- Interfaces were unreliable or unnecessarily complicated.
- Hardware companion apps sometimes failed to connect.
- Ads were intrusive or inappropriate.
- Users felt misled when an app implied that digital zoom turned a phone into a real microscope.
- Paywalls sometimes blocked core utility.

Positive reviews were equally useful. People valued reliable manual focus, exposure control, saving images, simple operation, support for ordinary microscope adapters, and classroom or group-viewing workflows.

The resulting positioning was not another general magnifier. It was a focused camera utility for a real microscope workflow.

That distinction shaped everything that followed.

## Research became a set of product constraints

I documented the product before scaffolding the Xcode project. The core positioning was deliberately literal:

> Use your iPhone with a compatible microscope eyepiece adapter to view and record what your microscope sees.

The app would not claim that an iPhone alone becomes an optical microscope. It would not connect to Wi-Fi or USB microscopes. It would not offer OCR, AI specimen identification, medical diagnosis, calibrated measurement, scale bars, or scientific reporting.

Those exclusions were not a lack of ambition. They protected the product from becoming a collection of loosely related camera features and prevented the App Store listing from promising things the app could not honestly deliver.

The MVP came down to four jobs:

1. Help the user align the correct iPhone camera with a microscope eyepiece.
2. Provide a clean, reliable live view.
3. Capture native photos and videos.
4. Offer precision controls when the native Camera app was not sufficient.

The free version would include the functional core: live viewing, zoom, tap to focus, photo capture, video recording, and a fixed Center Marker. Pro would unlock manual focus, exposure, supported white-balance controls, additional capture-quality options, and Center Marker customization.

## Market evidence shaped the business model

The market analysis also helped determine the purchase options, pricing, and division between Free and Pro.

The researched competitors ranged from entirely free utilities to apps using advertising or small one-time upgrades. Their negative reviews included intrusive ads and frustration with paywalls blocking core utility. The resulting recommendation was to keep the basic microscope workflow useful and monetize advanced controls.

The final Free tier includes live viewing, basic zoom, tap to focus, photo capture, video recording, saving, and a fixed Center Marker. Pro adds manual focus, exposure, supported temperature and tint controls, Center Marker customization, additional supported photo and video quality choices, and capture-mode App Shortcuts.

Both purchase options unlock the same Pro feature set:

- **Monthly:** $1.99 per month in the US, without an introductory trial.
- **Lifetime:** a $9.99 one-time purchase in the US.

Lifetime is selected by default and presented as **Best Value**. Monthly remains the lower-upfront option. The paywall shows only verified live StoreKit prices and never substitutes hard-coded fallback pricing.

Privacy became another constraint: no ads, no account, no analytics SDK, no tracking, and no developer-operated upload of camera frames or captures.

<!-- Publishing asset source: screenshots/final/English/02-view-through-your-microscope.png -->
<img src="/assets/images/microscope-app-02-live-view.jpg" alt="Microscope App live viewer showing a botanical cross-section through an iPhone microscope view" width="62%" style="display:block; margin:1.5rem auto 0.75rem; border-radius:18px;" />

*The released viewer stays focused on the microscope image, with capture controls and alignment tools kept around the edge.*

## The first product problem was setup, not capture

A conventional camera app can assume that the user points the phone at a subject. Microscope App cannot. The user must own an adapter, mount the iPhone, identify the rear 1× Main camera, position that camera over the eyepiece, grant permission, align the circular image, and confirm that the setup works.

The final onboarding flow uses five milestones: Prepare, Explore, Connect, Capture, and Review.

It asks the user to prepare the microscope and adapter, records the intended use cases, provides device-aware physical positioning guidance, explains privacy and camera access, opens an alignment workspace, and lets the user make a trial photo or silent video. The user then reviews the unaltered capture and decides whether to save it or adjust the alignment.

Permission timing was designed around intent. The app may inspect camera capability when the user enters setup, but it does not prompt automatically. Camera access is requested only after the user chooses **Start Live View**. Photos access is requested later, only after the user accepts a valid capture and chooses to save it. Microphone access is an optional main-viewer preference and is never requested during onboarding.

## The Codex app worked from explicit repository constraints

I used Codex during implementation and verification. The repository supplied the constraints for that work: product scope, onboarding state transitions, locked design decisions, App Store metadata, localization rules, accessibility evidence, privacy claims, and interaction invariants. Reusable product-neutral mechanics belonged in IndieAppKit; microscope-specific copy, navigation, camera behavior, permissions, and purchase configuration remained in the app.

This made each Codex-assisted change reviewable against a written source of truth. Camera behavior could be checked against the PRD and onboarding specifications, localized content against the string catalogs and metadata handoff, and release claims against the verification and audit reports.

## The camera was the real engineering challenge

The visible interface is deliberately restrained, but the camera system underneath it is stateful and timing-sensitive.

Microscope App uses the physical rear 1× Wide camera throughout the workflow. It discovers real capture formats at runtime, validates saved preferences against the current device, prepares photo or video capture before enabling the shutter, and uses native AVFoundation outputs rather than processing a continuous stream of camera frames.

The app also separates the onboarding camera session from the long-lived main viewer. They never run simultaneously. After a trial capture, onboarding stops and dismantles its camera graph before presenting Review & Save. Entering the main viewer creates a fresh preview and camera lease rather than carrying hidden onboarding state into the permanent experience.

The documented lifecycle rules cover foregrounding, backgrounding, permission changes, video recording, capture settlement, format selection, paywall presentation, and temporary preview loss. The viewer records the newest user intent, serializes access to the physical session, distinguishes a running capture session from a rendering preview, and permits only bounded automatic recovery.

Photo and video capture are transaction-scoped. A video is not considered recording until AVFoundation confirms that recording started. An early stop is accepted once, draft media remains alive until a terminal callback, and a failed recording returns to the live viewer rather than unnecessarily rebuilding the entire camera experience.

The precision controls also depend on hardware capability. Every supported device receives Zoom, Focus, and Exposure. Temperature and Tint appear only when the physical camera supports custom locked white-balance gains. Photo resolutions and 30/60 fps video profiles are derived from exact formats supported by the current device rather than from a hard-coded menu.

<!-- Publishing asset source: screenshots/final/English/03-capture-photos-and-video.png -->
<img src="/assets/images/microscope-app-03-capture.jpg" alt="Microscope App configured for video recording with a specimen visible through the microscope" width="62%" style="display:block; margin:1.5rem auto 0.75rem; border-radius:18px;" />

*Photo and video share one minimalist viewer, while the format label reflects the actual prepared capture profile.*

## The Simulator could not prove that the product worked

Automated tests could validate reducers, persistence, routing, permission gates, localization, StoreKit behavior, and deterministic UI states. A fake camera service could reproduce success and failure paths. None of that could verify the most important promise: that a physical iPhone camera would reliably show and capture a real microscope view.

The iOS Simulator has no usable rear camera. Real discovery, permissions, preview behavior, focus, exposure, white balance, recording, microphone timing, and haptics therefore required a physical device.

The project used Simulator automation for deterministic coverage and my physical iPhone 17 for live-camera conclusions. The Codex app used Xcode tooling with that connected iPhone to run the physical-device test workflows. The recorded matrix covered the real camera, permissions, appearance, accessibility settings, assistive technologies, and the shared Adjust panel over varied live scenes. The release matrix also included a local Release archive and the production build distributed through TestFlight.

## Accessibility changed the design

Accessibility was not a final checklist applied after the interface had settled. The audit exposed layout and contrast problems that changed the product.

The dedicated suite covered the major onboarding and viewer states across multiple iPhone sizes, Light and Dark appearances, Dynamic Type sizes up to AX5, forced right-to-left layout, and all eight launch languages. It added semantic assertions for labels, selected states, locked controls, slider values, and minimum control sizes.

The work led to concrete corrections. Onboarding actions moved into the scroll flow at accessibility sizes. Use-case rows became full-width semantic controls. Settings and camera adjustment layouts learned to wrap and scroll. Hidden controls were removed from the accessibility hierarchy. Localized recovery text was shortened where it failed at AX5. Camera controls gained better contrast protection.

One of the recorded corrections involved the Adjust panel. An early translucent surface could not guarantee readable controls over every possible microscope image. The final shared panel uses an opaque semantic system background and native label colors.

The released baseline passed 45 app-owned accessibility tests, the paywall's Light, Dark, and AX5 variants, physical-device checks with assistive technologies, live-camera contrast checks, and the TestFlight production matrix.

## Localization was a product and layout exercise

Version 1.0 launched in English, Brazilian Portuguese, Spanish, French, Italian, German, Danish, and Finnish.

The localization work covered more than the App Store description. It included the app interface, permission explanations, onboarding, paywall and product metadata, App Shortcuts, promotional text, keywords, screenshot captions, and reviewer instructions.

The release process verified 326 localized entries across all eight locales, checked placeholder parity, exercised pseudolocalization and forced RTL, and captured deterministic screenshots at large Dynamic Type sizes. Apple Translation generated the available first-pass translations, and a semantic back-translation spot check with the Codex app helped find literal or inconsistent high-visibility strings.

There is still an honest limitation: the launch translations did not receive complete native linguistic review. That remains a documented risk rather than something the release process pretends to have solved.

## App Store artwork was part of product positioning

The released screenshot direction starts with a copy-free microscope-and-mounted-iPhone hero. The remaining images demonstrate live viewing, photo and video capture, and practical use cases.

The six-screen sequence became:

1. Turn your microscope into a camera.
2. View through your microscope.
3. Capture photos and video.
4. Inspect electronics up close.
5. Examine gems and collectibles.
6. Show every detail.

The campaign uses generated representative hardware and specimen compositions across those scenarios. The product UI inside the device reflects the released app, while the captions avoid medical, calibrated-measurement, and phone-as-microscope claims.

<!-- Publishing assets:
screenshots/final/English/04-inspect-electronics-up-close.png
screenshots/final/English/05-examine-gems-and-collectibles.png
screenshots/final/English/06-show-every-detail.png
-->
<div style="display:flex; flex-wrap:wrap; gap:0.75rem; align-items:flex-start; margin:1.5rem 0 0.75rem;">
  <img src="/assets/images/microscope-app-04-electronics.jpg" alt="Microscope App App Store artwork demonstrating electronics inspection" style="flex:1 1 180px; min-width:0; border-radius:12px;" />
  <img src="/assets/images/microscope-app-05-gems.jpg" alt="Microscope App App Store artwork demonstrating gemstone and collectible examination" style="flex:1 1 180px; min-width:0; border-radius:12px;" />
  <img src="/assets/images/microscope-app-06-detail.jpg" alt="Microscope App App Store artwork demonstrating detailed specimen viewing" style="flex:1 1 180px; min-width:0; border-radius:12px;" />
</div>

*Representative App Store marketing compositions showing three intended workflows: electronics inspection, gems and collectibles, and detailed specimen viewing.*

The artwork and captions were then localized into the eight launch languages. Metadata followed the same evidence-based positioning. The name remained **Microscope App**, the subtitle became **Camera for Photo & Video**, and keyword fields prioritized the microscope-adapter niche instead of using every available character for broad traffic.

## Shipping meant finishing the unglamorous work

The remaining work included StoreKit 2 product validation, Monthly and Lifetime purchase paths, restore behavior, entitlement persistence, privacy labels, the privacy manifest, localized Camera, Photos, and Microphone purpose strings, export-compliance declarations, legal and support pages, App Review notes, signing, archive inspection, TestFlight, sandbox purchase validation, and release verification.

The command-line StoreKit Test environment also produced an Xcode internal error and could block on system purchase UI. Instead of recording the interrupted runner as a pass, I documented the limitation and validated the affected purchase and restore paths through Xcode and TestFlight sandbox.

This kind of evidence matters because an App Store product is larger than its source code. A local build cannot prove that live StoreKit products are available, that signing is correct, that permission copy appears as intended, or that the production binary behaves like the Debug app.

Version 1.0 build 5 completed that release path and became publicly available on August 6, 2026.

The app waited nine days before its App Store Connect status changed to **In Review**. Once the review began, Apple approved it in about one hour without requesting any clarification.

## What the release evidence shows

### Start with complaints, not feature ideas

Competitor reviews documented problems with blurry focus, unreliable behavior, complicated interfaces, intrusive ads, hardware connections, and misleading microscope expectations. The released scope directly addresses those themes through manual controls, explicit adapter requirements, guided setup, and privacy-first positioning.

### Non-goals constrained implementation and claims

The PRD explicitly excludes diagnosis, measurement, scanners, Wi-Fi and USB microscope support, cloud sync, and other adjacent features. Those non-goals kept the implementation and App Store claims aligned with an iPhone eyepiece-adapter camera utility.

### Physical products need physical validation

Simulator automation covered deterministic states, while the connected physical iPhone 17 covered the real camera and device-dependent behavior. TestFlight covered the production build and StoreKit sandbox path. The audit records those as separate forms of evidence.

### Accessibility is a design input

Large text, contrast, semantic controls, RTL behavior, and assistive technologies led to the layout and surface corrections recorded in the accessibility audit.

### Marketing assets should clarify the product

The generated artwork demonstrates varied specimens and use cases, while the captions, description, and opening hero retain the physical adapter requirement and the documented limits of the app.

### The Codex app ran across multiple verification environments

The Codex app assisted the implementation and verification workflow, ran test workflows against my physical iPhone 17, supported localization checks, and contributed to the generated marketing campaign. The release still depended on the recorded Simulator, physical-device, archive, StoreKit, TestFlight, and App Review evidence.

## The app shipped; the next evidence comes from users

The repository contains no post-launch discovery, retention, or paid-conversion results, so this article does not claim them. Those outcomes require evidence beyond the quality of the code or the speed of the launch.

The documented process turned Astro keyword evidence into a focused native iPhone product. The app now guides a user through a real microscope setup, provides a live viewer, captures native photos and videos, offers paid precision controls while retaining a functional Free tier, and makes explicit promises about privacy and scope.

The sequence began with Astro market research, continued with the registration of **Microscope App** in App Store Connect and the competitor analysis, and ended with the App Store release on August 6. The repository between those points records the product decisions, implementation, tests, corrections, metadata, and release evidence.

The Codex app was part of that build, including tests run on the physical iPhone 17. The market evidence defined why the product was worth exploring; the repository evidence defined what could truthfully be claimed when it shipped.
