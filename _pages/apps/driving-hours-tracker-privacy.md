---
layout: page-custom
title: "Driving Hours Tracker Privacy Policy"
seo_title: "Driving Hours Tracker Privacy Policy"
description: "Learn how Driving Hours Tracker handles learner records, private routes, location, iCloud synchronization, PDFs, subscriptions, Apple system surfaces, diagnostics and support communications."
permalink: /apps/driving-hours-tracker/privacy
author_profile: false
analytics: false
remove_heading_permalinks: true
classes: [legal-page]
canonical_url: https://sahilsatralkar.com/apps/driving-hours-tracker/privacy
locale: en-GB
---

**Effective date:** 28 August 2026

This Privacy Policy explains how the Driving Hours Tracker app handles learner information, driving records, location, iCloud synchronization, purchases, system surfaces, diagnostics, PDFs, and support communications.

## Overview

Driving Hours Tracker does not operate a separate developer account system or a developer-operated server for learner logbook content.

Depending on how you use the app, information is stored:

- locally on your iPhone;
- in your private iCloud database for eligible synchronization between your iPhones; or
- in a PDF outside the app when you choose to create or share one.

Driving Hours Tracker uses RevenueCat to provide subscription products and determine Full Access.

The app does not contain advertising, cross-app tracking, or custom product-usage analytics. Learner details, drives, routes, locations, goals, cars, Notes, PDFs, and the free-drive allowance are not sent to RevenueCat.

## Information you enter

Driving Hours Tracker may store information that you choose to enter, including:

- a learner display name;
- an optional permit or reference value;
- personal total-hours and night-hours goals;
- a Miles or Kilometers preference;
- car names and the Selected Car;
- Weather, Roads, and Skills selections; and
- Notes about a drive.

Do not enter passwords, payment-card information, Apple Account credentials, medical information, or other unnecessary sensitive information in these fields.

## Drive and route information

When you use Start and Finish, the app may create and store:

- random record and installation identifiers;
- Start and Finish times;
- elapsed duration and time-zone context;
- the surface that issued a command, such as iPhone, widget, or CarPlay;
- the selected car identifier and name captured at Start;
- review state and revision times;
- route status and quality information;
- timestamped location coordinates and horizontal-accuracy values when location is available;
- a derived Estimated Distance and calculation provenance;
- estimated Day, Night, and Unclassified durations;
- privacy-reduced start and end information;
- schema, integrity, conflict-resolution, deletion, and synchronization metadata; and
- the descriptive practice information listed above.

Exact timestamped route coordinates are treated as highly sensitive. They are used for the private in-app route, Estimated Distance, Night Estimate, route-quality disclosure, integrity checks, and private iCloud synchronization.

Exact routes and coordinates are not included in widgets, Live Activities, CarPlay, notifications, routine diagnostics, RevenueCat data, PDFs, or external route links.

## Local storage

The local logbook is the authoritative record for an active drive. Driving Hours Tracker stores app data in its iOS app container using a Core Data SQLite store and device-local preferences.

The app uses iOS Data Protection compatible with the background access needed to keep an active drive durable. No storage system can guarantee that data will never be lost or accessed unlawfully.

Device-local information can include:

- onboarding progress and setup drafts;
- an active drive and unsynchronized route samples;
- local synchronization state;
- a one-way hash derived from the current iCloud user record identifier, used to keep different Apple Account datasets isolated;
- locally accepted Full Access evidence through its known expiry; and
- compact widget and Live Activity projections.

The app does not use the iCloud account hash as an advertising identifier or send it to RevenueCat.

Deleting the app normally removes its local app container and device-local preferences. Unsynchronized data, including an active drive, may then be unrecoverable. Deleting the app does not automatically remove data already stored in private iCloud or cancel a subscription.

## Location

Driving Hours Tracker asks for location access in context when a drive starts from the iPhone or widget. A CarPlay Start does not trigger a location-permission prompt on the vehicle display.

When permission and iOS allow it, the app records location during an active drive, including while the app is in the background. iOS may show its background-location indicator. The app records timestamped coordinates and accuracy values in small local batches.

Location is used to:

- draw the private in-app route;
- calculate a best-effort Estimated Distance;
- calculate a best-effort Night Estimate;
- identify route gaps or reduced accuracy; and
- derive privacy-reduced start and end information for the app and PDF.

Location is optional for time recording. If you deny or revoke permission, the timer and Finish can still work, while route, distance, endpoint, or night information may be limited, unavailable, or Unclassified.

You can review or change location permission in iPhone Settings.

## Estimated Distance and Night Estimate

Estimated Distance is derived locally from accepted consecutive location samples within captured route segments. The app does not use a planned Apple Maps route, fill a substantial GPS gap, or substitute a straight line between the first and last point.

Night Estimate is calculated locally from available time, location, and time-zone evidence. Inconclusive time is stored as Unclassified rather than being guessed.

The app stores calculation versions and quality information so results can be explained consistently. These results are estimates, not verified odometer or legal-night-hours values.

## iCloud synchronization

When an Apple Account and iCloud are available, Driving Hours Tracker uses Apple's private CloudKit database to synchronize eligible logbook information between iPhones signed in to that account.

Eligible synchronized information includes:

- finished drives and their exact private routes;
- Estimated Distance, Night Estimate, route-quality, and calculation information;
- Needs Review drafts and Reviewed state;
- learner report details and personal goals;
- car profiles and the Selected Car;
- the Miles or Kilometers preference;
- deletions and logbook-generation information; and
- a privacy-minimal record of whether the one free drive is available or used.

Active drives are not synchronized and cannot be controlled or finished remotely from another iPhone.

Driving Hours Tracker uses private iCloud data only. It does not create a shared family logbook or send learner content to a separate developer-operated server. Apple Family Sharing shares eligible subscription access only, not learner data or the free-drive allowance.

Synchronization is asynchronous. It may be delayed or unavailable because of the network, iCloud capacity, Apple Account state, device settings, or Apple service conditions. Locally authorized recording and locally available records remain usable when iCloud is unavailable.

A minimal deletion tombstone or logbook-generation record may remain in private synchronization data to prevent an old offline device from restoring deleted content. A drive tombstone contains only identifiers and deletion-generation information needed for that purpose, not its time, route, car, or descriptive content.

Apple handles iCloud information under its [Privacy Policy](https://www.apple.com/legal/privacy/).

## Apple Maps and system services

Driving Hours Tracker uses Apple MapKit to present a route inside the app. It may open the Apple Maps app after Start when you choose that handoff. Driving Hours Tracker does not store the destination you choose in Apple Maps or import a planned route as recorded evidence.

Map tiles, system-provided place information, and Apple Maps interactions are supplied by Apple and may require network access. Apple handles those services under its [Privacy Policy](https://www.apple.com/legal/privacy/).

## Widgets, Live Activities, and CarPlay

Driving Hours Tracker can place a compact projection in its private app group so its widget can show setup or access state, learner name, Selected Car, total recorded time, a personal goal, and active-drive status where appropriate.

A Live Activity can contain a random drive identifier, the captured car name, and the Start time needed to show recording status and elapsed time.

Eligible CarPlay systems can show limited setup, access, Selected Car, recording, elapsed-time, and Finish information through the running app.

These are Apple-managed system surfaces. Their visibility depends on your device, Lock Screen, widget, Live Activity, notification-preview, CarPlay, and vehicle settings. They never receive the exact route from the app.

## PDFs and sharing

Driving Hours Tracker generates PDF practice records locally from data available on the iPhone.

A PDF can contain:

- the learner display name and optional permit or reference;
- the selected date range and generation time;
- goals, totals, statuses, and quality disclosures;
- drive times, durations, Estimated Distance, Night Estimate, and Unclassified time;
- privacy-reduced start and end information;
- captured car names and descriptive practice details; and
- product disclaimers.

A PDF never contains exact coordinates, street addresses, route geometry, route thumbnails, or route links.

When you share or save a PDF through the iOS share sheet, the destination you choose receives a copy. That copy is outside the app's control and cannot be recalled, changed, or deleted by Driving Hours Tracker.

## Purchases and RevenueCat

App Store purchases and subscriptions are processed by Apple. We do not receive your payment-card details or Apple Account password.

Driving Hours Tracker uses RevenueCat to load subscription products, process purchase results, restore eligible purchases, determine Full Access, and keep entitlement state current.

RevenueCat generates a random anonymous App User ID for the installation. Driving Hours Tracker does not display that identifier and does not set a name, email address, or other customer attribute on it.

RevenueCat may receive:

- the anonymous App User ID;
- App Store product, offering, purchase, transaction, and receipt information;
- subscription, trial, Family Sharing ownership, renewal, expiry, and entitlement status; and
- SDK-required app, platform, operating-system, store, locale, currency, network, and service metadata.

Driving Hours Tracker does not deliberately send RevenueCat:

- a learner name, email address, or permit reference;
- an Apple Account or iCloud identifier;
- an iCloud account hash or CloudKit record identifier;
- a drive, route, coordinate, endpoint, or location-permission state;
- Estimated Distance, Distance Unit, Night Estimate, or goal information;
- a car name or identifier;
- Weather, Roads, Skills, or Notes;
- a PDF or PDF selection;
- free-drive allowance state or consumption events;
- customer attributes;
- advertising identifiers;
- attribution data; or
- custom product-usage, onboarding, or paywall-impression events.

Automatic device-identifier collection and RevenueCat diagnostics are disabled in the app configuration. Driving Hours Tracker does not enable RevenueCat advertising integrations, attribution integrations, custom webhooks, or exports without a separate review and an updated disclosure.

RevenueCat handles information under its [Privacy Policy](https://www.revenuecat.com/privacy-policy).

Apple handles App Store and purchase information under its [App Store & Privacy information](https://www.apple.com/legal/privacy/data/en/appstore/) and [Privacy Policy](https://www.apple.com/legal/privacy/).

## Family Sharing

Eligible Driving Hours Tracker subscriptions may support Apple Family Sharing.

Apple determines family membership, purchase sharing, and subscription eligibility. Driving Hours Tracker receives only the purchase and entitlement evidence needed to determine whether Full Access is active.

Family Sharing provides access only. It does not disclose or combine learner names, permit references, logbooks, drives, routes, cars, goals, PDFs, or free-drive allowances between family members.

## Diagnostics and App Store metrics

Driving Hours Tracker does not include third-party crash-reporting, advertising, attribution, or general product-analytics SDKs.

If you choose to share analytics or diagnostics with developers through your Apple settings, Apple may make crash, hang, launch, performance, and aggregate app information available through its developer services. Do not include learner or route content when you voluntarily send a screenshot, recording, or support message.

Apple may provide aggregated App Store acquisition and product-page information. RevenueCat may provide purchase-derived subscription, trial, renewal, churn, and revenue information. Driving Hours Tracker does not add custom learner, drive, location, onboarding, or app-usage events to those metrics.

The app does not request App Tracking Transparency permission, access IDFA, sell learner information, or perform cross-app or cross-website tracking.

## When you contact support

If you email us, we receive the email address, message, and attachments that you choose to provide.

We use support information only to:

- respond to your request;
- troubleshoot the app;
- investigate purchase or restoration issues;
- protect the app and its users; or
- meet applicable legal obligations.

Support correspondence is retained only for as long as reasonably needed for those purposes.

Email is transmitted and stored through the email providers used by you and by us. Do not send Apple Account passwords, payment-card details, App Store receipts, permit information, learner records, exact locations, route screenshots, PDFs, or other sensitive content.

## How information is used

Information handled by Driving Hours Tracker is used to:

- create and maintain a local learner logbook;
- record and recover active drives;
- calculate durations, route quality, Estimated Distance, and Night Estimate;
- show History, totals, review status, and personal-goal progress;
- synchronize eligible data through private iCloud;
- provide requested widget, Live Activity, CarPlay, Apple Maps, and PDF features;
- verify Full Access and the one-free-drive allowance;
- restore eligible purchases; and
- respond to support requests.

We do not sell learner information or use it for advertising.

## Retention

Local logbook information remains on the iPhone until it is changed, deleted through an applicable app flow, erased with the logbook, or removed with the app.

Cloud-backed information remains in private iCloud until it is deleted, the logbook is erased, or Apple applies its own retention rules. Synchronization and deletion may be delayed while a device or iCloud is offline.

Completed records remain until you delete a drive or erase the logbook. Privacy-minimal tombstones may remain for the life of the current logbook generation. The free-drive allowance is intentionally separate from the erasable logbook and is not reset by deleting a drive or erasing the logbook.

Apple and RevenueCat retain purchase and service information according to their respective policies and legal obligations.

Support correspondence is retained only as long as reasonably necessary for support, security, and legal purposes.

PDF copies remain wherever you choose to save or share them and are outside the app's retention control.

## Deleting information

You can delete an individual drive from History or Drive Detail. Confirmed deletion removes the drive, its exact route, and its derived results from the current logbook. There is no app-provided undo or Recently Deleted area. A privacy-minimal synchronization tombstone may remain to prevent stale restoration.

You can use **Settings → Erase Logbook Data and Start Over** to remove the current learner logbook locally and from private iCloud where possible. This action is unavailable during Recording or Finalizing. It does not cancel or refund a subscription, change Full Access, or restore a used free-drive allowance. Previously shared PDFs remain outside the app's control.

Deleting the app normally removes its local app container but does not automatically remove information already stored in private iCloud, cancel an App Store subscription, delete Apple or RevenueCat purchase records, or recall a shared PDF.

## Your choices

You can:

- allow or deny location access in iPhone Settings;
- keep recording time when location is unavailable;
- control iCloud access through Apple settings;
- delete individual drives;
- erase the current logbook through the app when no drive is Recording or Finalizing;
- choose whether to create, save, or share a PDF;
- add, edit, or omit optional learner and practice details before they become locked;
- manage or cancel subscriptions through Apple;
- restore eligible purchases;
- delete the app's local data by deleting the app; and
- contact us with a privacy question.

Requests concerning Apple Account, iCloud, App Store, Apple Maps, Family Sharing, or Apple diagnostic information should also be directed through Apple's privacy and account controls.

## Children's privacy

Driving Hours Tracker does not ask for a user's age and does not operate a developer account, advertising service, or shared family logbook.

A learner display name is stored locally and may synchronize through the learner's private iCloud account. It is not deliberately sent to the developer or RevenueCat.

If a child is not old enough to manage the app and its records independently where they live, a parent or legal guardian should supervise its use. If you believe a child has sent personal information to the support email, contact us so that we can review and delete it where appropriate.

## Changes to this policy

We may update this policy when the app's behaviour, service providers, or legal requirements change.

The revised policy will be posted at this URL with a new effective date.

## Contact

For privacy questions, email <!--email_off--><a href="mailto:priya.satralkar8@gmail.com">priya.satralkar8@gmail.com</a><!--/email_off-->.

## Legal documents

- [Driving Hours Tracker Terms of Use](https://sahilsatralkar.com/apps/driving-hours-tracker/terms)
- [Driving Hours Tracker Support](https://sahilsatralkar.com/apps/driving-hours-tracker/support)
