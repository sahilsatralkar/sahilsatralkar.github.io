---
layout: single
title: "I Built a Cold Plunge App with AI. The App Shipped; the Business Didn’t—Yet"
date: 2026-08-01
permalink: /blog/building-cold-plunge-timer-log-with-ai/
categories: [iOS Development, Indie Development, AI]
tags: [SwiftUI, StoreKit 2, ASO, SEO, Codex, IndieAppKit, App Store]
header:
  teaser: /assets/images/cold-plunge-app-icon.png
---

In May 2026, I started building a focused iPhone app for cold plunges. I released it on the App Store on June 25. I am writing this retrospective just over a month later. In that short period, I migrated its purchase system, localized it, built a separate marketing website, published a growing library of search-focused articles, produced social assets, and watched several of my target keywords climb.

What I did not have was a successful business.

That distinction matters. Shipping an app is an engineering result. Getting discovered is a distribution result. Convincing someone to pay is a product and positioning result. I made progress on the first two and fell short on the third.

This is the complete journey so far: how I chose the niche, how I used AI and Codex as a development partner, what I built, what I marketed, what ranked, what failed, and what I would do differently as an independent iOS developer.

> Disclosure: I am deliberately not publishing download, revenue, or subscription counts. I will share keyword rankings and public website-search trends because they are useful to other developers.

The live product and public work are here:

- [Cold Plunge Timer & Log on the App Store](https://apps.apple.com/us/app/cold-plunge-timer-log/id6768260349)
- [Cold Plunge Timer & Log website](https://coldplungetimerapp.com/)
- [Cold Plunge Guides](https://coldplungetimerapp.com/blog/)

<img src="/assets/images/cold-plunge-app-icon.png" alt="Cold Plunge Timer & Log app icon" width="180" style="display:block; width:42%; max-width:180px; margin:1.75rem auto 0.75rem; border-radius:22%;">

*The final app icon: a restrained wave mark designed to match the calm, native character I wanted for the product.*

## I started with search intent, not a feature idea

The thesis was simple: people already searching for a “cold plunge timer,” “cold plunge tracker,” “ice bath timer,” or “cold plunge log” have a specific problem. A generic stopwatch records elapsed time, but it does not remember water temperature, notes, streaks, or progress.

I researched existing apps and their public marketing footprints. The niche had competitors, but no obvious winner owned every channel. Some had polished products, some had useful content, and some had wearable integrations, but the category still looked fragmented.

My initial high-intent keyword cluster was:

- `cold plunge timer`
- `cold plunge tracker`
- `ice bath timer`
- `ice bath tracker`
- `cold plunge log`

That research shaped the product before I wrote the main app. I locked the name as **Cold Plunge Timer & Log** and the subtitle as **Temp, Progress, Streak Tracker**. The metadata was not decoration added at submission time. It was an early product constraint.

This was useful, but it also planted the seed of a mistake: I became very good at optimizing around a keyword-shaped product before proving that the audience behind those searches had strong willingness to pay.

## Reducing the product to Timer, Log, and Stats

The early product document contained more ambitions than the app needed: sharing, milestones, challenges, widgets, Live Activities, Dynamic Island, Apple Watch, and broader cold-exposure routines.

The version that became coherent was much smaller:

1. **Timer** — begin a session quickly, set an optional goal, and continue beyond it.
2. **Log** — save duration, water temperature, date, and notes.
3. **Stats** — review sessions, progress, and streaks.

Settings became the fourth tab, but not a fourth product pillar.

The design direction was deliberately native: SwiftUI, SF Symbols, semantic colors, Dynamic Type, light and dark appearance, and a restrained blue accent. I wanted the app to feel calm and specific, not like a gamified workout dashboard or a generic wellness template.

<img src="/assets/images/cold-plunge-timer-running.png" alt="Cold Plunge Timer running in the iPhone 17 simulator with the progress ring active" width="62%" style="display:block; margin:1.5rem auto; border:1px solid #ddd; border-radius:18px;">

*The current Timer screen after a little over a minute. The ring makes progress visible while the primary control stays focused on pausing the session.*

## Building the app—and accidentally building a framework

I was not only building Cold Plunge. I also wanted reusable foundations for future indie apps: onboarding, preferences, purchases, paywalls, notifications, haptics, review prompts, and local-data deletion.

That work became **IndieAppKit**, a private Swift package consumed by the app as a pinned release. The boundary I eventually settled on was:

- IndieAppKit owns reusable mechanics.
- Cold Plunge owns product meaning.

The app owns its product IDs, copy, links, feature identifiers, StoreKit adapter, timer behavior, SwiftData session model, and routing. The kit owns reusable protocols and configurable UI foundations.

This separation is one of the parts I am happiest with technically. It is also a place where AI assistance can become dangerous. Codex is very capable of seeing patterns and proposing abstractions. It is less naturally resistant to premature generalization unless I give it strong boundaries.

My rule became: code belongs in the kit only if it is product-neutral, configurable, independently testable, and plausibly reusable by at least two unrelated apps. Otherwise it stays in the host app.

The resulting architecture used:

- SwiftUI with feature-oriented MVVM
- SwiftData for local session history
- app-owned adapters around system services
- typed preferences instead of direct settings access from screens
- deterministic launch arguments for UI testing
- stable accessibility identifiers
- StoreKit test configuration for purchase scenarios

The privacy promise was equally important: no account, no ads, no tracking, and local-first app data.

## AI was a collaborator, not an autocomplete box

Codex participated in almost every layer of the project:

- product requirements and scope reduction
- competitor and keyword research
- SwiftUI implementation and refactoring
- unit and UI tests
- accessibility audits
- localization drafts
- App Store metadata and screenshot production
- website design and implementation
- SEO article research and publishing
- marketing trackers and campaign assets

That breadth created enormous leverage. I could move from a product question to a code change, a test, a screenshot, a website update, and a marketing artifact without handing context between several people.

It also created new failure modes.

In one website discussion, Codex started implementing before I had approved the direction. I stopped it and asked it to discard the changes. In other cases, it produced technically competent output that was strategically premature: more content, more localizations, more infrastructure, or more reusable code before the market had earned that investment.

AI makes execution cheaper. It does not make every executable idea worth executing.

The quality of the project improved when I treated decisions as explicit constraints: locked product naming, precise free-versus-Pro rules, no unsupported medical claims, no hardcoded production prices, app-owned navigation, and verification commands written into repository instructions.

## Monetization: clear in code, unclear in the market

The free timer remained unlimited. Pro gated saving sessions, adding manual sessions, and building real history and progress. Existing local data stayed readable if entitlement expired. I wanted the paywall to sell continuity, not hold the basic timer hostage.

The app launched with monthly, yearly, and lifetime plans. Yearly was selected by default, with its savings and monthly equivalent calculated from matching-currency StoreKit metadata rather than parsed price strings.

The first purchase implementation used RevenueCat behind an app-owned abstraction. That architecture made the later decision easier: when the service added no meaningful value for the app’s actual commercial state, I removed it and migrated to direct StoreKit 2. The reusable package stayed SDK-neutral; the concrete StoreKit adapter stayed in the app.

That migration shipped in version 1.0.4.

Technically, it was a success. Commercially, the app had underperformed my expectations. I had built a careful paywall and a robust entitlement system before proving that the product’s paid value was compelling enough.

The lesson was uncomfortable: a clean purchase architecture cannot rescue weak purchase intent.

## Accessibility and localization became real product work

Accessibility was not a submission-day checklist. I worked through VoiceOver, Voice Control, Larger Text, Dark Interface, non-color differentiation, contrast, and Reduced Motion. I added meaningful labels and values, fixed duration controls, checked whole-row tap targets, and captured large-text verification screens across key flows.

The app eventually supported 15 in-app languages. AI produced the first drafts, but the repository documentation is honest about their status: non-English translations should receive native-speaker review before paid acquisition.

Localization exposed real bugs rather than merely translating strings. Temperature-unit conversion, layout pressure, placeholder preservation, and app-versus-package string ownership all needed engineering attention.

I also localized App Store keywords and produced regional screenshot sets. The visible app name and subtitle remained English, while keyword fields used local-language opportunities where the evidence supported them.

<img src="/assets/images/cold-plunge-appstore-timer.png" alt="Cold Plunge Timer and Log App Store screenshot showing the timer" width="62%" style="display:block; margin:1.5rem auto; border:1px solid #ddd; border-radius:18px;">

*The first screenshot had one job: communicate the core timer immediately.*

<img src="/assets/images/cold-plunge-appstore-log.png" alt="Cold Plunge Timer and Log App Store screenshot showing session logging" width="62%" style="display:block; margin:1.5rem auto; border:1px solid #ddd; border-radius:18px;">

*The second screenshot connects the timer to the paid value: remembering temperature and session details.*

<img src="/assets/images/cold-plunge-appstore-progress.png" alt="Cold Plunge Timer and Log App Store screenshot showing routine and progress tracking" width="62%" style="display:block; margin:1.5rem auto; border:1px solid #ddd; border-radius:18px;">

*The third screenshot explains why the app is more than a stopwatch.*

<img src="/assets/images/cold-plunge-appstore-dark-mode.png" alt="Cold Plunge Timer and Log timer shown in dark mode" width="62%" style="display:block; margin:1.5rem auto; border:1px solid #ddd; border-radius:18px;">

*Dark mode was a real interface requirement, not a color inversion added to the App Store page. Semantic SwiftUI colors and native surfaces allowed the timer to retain its hierarchy in both appearances.*

<img src="/assets/images/cold-plunge-appstore-swedish.png" alt="Swedish localization of the Cold Plunge Timer interface and App Store screenshot" width="62%" style="display:block; margin:1.5rem auto; border:1px solid #ddd; border-radius:18px;">

*The Swedish screenshot is one example of the localization pipeline. App UI, screenshot headlines, controls, streak context, and metadata had to agree; the app name itself remained in English.*

## ASO results: narrow keywords did move

The first useful ranking snapshot came on June 21. In the United States, the app ranked:

| Keyword | Rank | Change in the recorded snapshot |
|---|---:|---:|
| `cold plunge streak` | 5 | +61 |
| `cold plunge progress` | 6 | +82 |
| `cold plunge timer` | 7 | +18 |
| `plunge timer` | 8 | +42 |
| `cold plunge log` | 8 | +36 |
| `cold plunge streak tracker` | 12 | New |
| `cold plunge app` | 43 | New |
| `cold plunge temperature` | 39 | +53 |

Those numbers validated part of the thesis: a focused title, subtitle, localized keyword fields, and aligned screenshots could make a new app visible for narrow category terms.

They did not validate the business.

Ranking for a low-popularity niche term is not the same as reaching a large market. Ranking also says nothing about whether the product page converts or whether the app’s paid proposition is strong after installation.

This is where ASO dashboards can give an indie developer false comfort. Green rank changes feel like momentum. Sometimes they are simply evidence that the chosen pond is small enough to move in.

## I built a second product: the marketing website

The website started as a small Astro landing page and became a substantial content system. It ran on Cloudflare Pages with custom-domain SSL, a sitemap, structured data, Search Console, Bing Webmaster Tools, an `llms.txt` file, manual IndexNow submission, and build-time SEO checks.

The design followed the same product rules: calm, native-feeling, concise, privacy-focused, and free of medical hype. The first version was not good. Spacing was awkward, the copy repeated itself, and the page felt like assembled sections rather than a designed product site. We paused implementation, wrote a design-and-copy direction, and rebuilt from that.

The content operation then expanded aggressively. By August 1, the site listed 18 published blog articles plus four app-focused guides. Topics ranged from practical duration and temperature questions to breathing, workout timing, DIY setups, streaks, Siri Shortcuts, and comparisons such as cold plunge versus cold shower.

The live site includes the [blog index](https://coldplungetimerapp.com/blog/) and app-focused guides such as:

- [Best Cold Plunge Timer App for iPhone](https://coldplungetimerapp.com/best-cold-plunge-timer-app-for-iphone/)
- [Using an Accessible Cold Plunge Timer App](https://coldplungetimerapp.com/accessible-cold-plunge-timer-app/)
- [Cold Plunge Tracker App](https://coldplungetimerapp.com/cold-plunge-tracker-app/)
- [Cold Plunge Timer with Siri Shortcuts](https://coldplungetimerapp.com/cold-plunge-timer-with-siri-shortcuts/)

Representative articles include:

- [How to Track Cold Plunge Sessions](https://coldplungetimerapp.com/blog/how-to-track-cold-plunge-sessions/)
- [Cold Plunge Timer vs Stopwatch](https://coldplungetimerapp.com/blog/cold-plunge-timer-vs-stopwatch/)
- [Cold Plunge Streak Tracker](https://coldplungetimerapp.com/blog/cold-plunge-streak-tracker/)
- [What Temperature Should a Cold Plunge Be?](https://coldplungetimerapp.com/blog/what-temperature-should-a-cold-plunge-be/)
- [How Long Should You Stay in a Cold Plunge?](https://coldplungetimerapp.com/blog/how-long-should-you-stay-in-a-cold-plunge/)
- [Cold Plunge vs Cold Shower](https://coldplungetimerapp.com/blog/cold-plunge-vs-cold-shower/)

The SEO trend improved:

| Seven-day snapshot | Impressions | Average position |
|---|---:|---:|
| July 8 | 69 | 39.9 |
| July 24 | 111 | 24.0 |
| August 1 | 118 | 23.3 |

The `cold plunge vs cold shower` article collected 28 impressions soon after publication. The before-bed article had 27, and the tracker-app page had 24 in the same later snapshot.

This was genuine progress: Google moved the site from roughly page four toward pages two and three and began matching it to several distinct intents.

It was not meaningful traffic yet. Most pages were still below the first page, where click-through rates are naturally weak. Publishing more pages created topical breadth, but it did not create authority by itself.

## Marketing plans versus marketing reality

The original organic plan had six pillars:

1. ASO
2. website and SEO
3. short-form video
4. communities
5. creator outreach
6. product-led sharing loops

In reality, I executed the first two far more deeply than the other four.

I created a public presence on [X](https://x.com/ColdPlungeTimer), [YouTube](https://www.youtube.com/@ColdPlungeTimer), [Facebook](https://www.facebook.com/people/Cold-Plunge-Timer-Log/61590648440016/), and Instagram. On X, I set up a focused brand profile, followed relevant cold-exposure accounts, published a founder/building-in-public post, and shared new articles. On YouTube, I created and branded the channel, wrote its description, linked the website and social profiles, and planned app-demo Shorts. On Facebook, I created and polished the Page with the app icon, website, support email, bio, call-to-action, cover artwork, and initial posts.

I also produced reusable campaign artwork for X and Facebook, including a seven-day cold-habit series and athlete-recovery and sauna-contrast concepts. I observed relevant Reddit communities rather than spamming links and built a repeatable image-composition workflow for different social safe zones.

But the existence of a YouTube channel did not become a consistent video engine. Posting on X and Facebook did not become a sustained distribution loop. Creator outreach did not become a real pipeline. Community work remained mostly observation. Several product-led sharing ideas stayed outside the shipped core.

This imbalance matters. I gravitated toward work that looked like engineering: structured content templates, automated screenshots, metadata matrices, build checks, image pipelines, and trackers. The work was useful and comfortable. Direct distribution—talking to creators, interviewing users, making repeated video, asking why someone would pay—was less comfortable, so it received less sustained attention.

The app did not fail because I lacked a marketing plan. It underperformed because the hardest parts of that plan were not executed with the same intensity as the parts that could be systematized in a repository.

## What I would do differently

### 1. Validate paid intent before building the full paid system

I would interview cold-plunge users and test the saving/history proposition before polishing three plan types, localized paywall copy, restore behavior, and entitlement-expiry edge cases.

### 2. Separate search opportunity from business opportunity

Low competition is attractive, but sometimes competition is low because demand or willingness to pay is low. I would score keywords alongside market size, existing paid behavior, retention frequency, and pain severity.

### 3. Delay broad localization

Localization improved the product, but 15 languages were too much before strong traction. I would start with the most defensible markets, validate conversion and retention, then expand.

### 4. Publish fewer articles and earn more authority

The website proved that disciplined content can gain impressions and improve average position. The next bottleneck is not another broad article. It is getting the best existing pages into the top ten through stronger distribution, relevant links, original evidence, and genuinely useful tools or data.

### 5. Treat creator outreach and video as product work

I treated them as marketing tasks that could wait until the app was ready. They should have run alongside development and influenced the product itself.

### 6. Use AI to compress feedback loops, not avoid them

AI was outstanding at turning decisions into implementation. It was also capable of helping me produce an impressive amount of output without requiring external validation. I need to use that speed to run more market experiments, not simply to build more assets.

## What I still consider a success

The commercial result has disappointed me, but I do not consider the project wasted.

I shipped a real native iOS product, built a reusable package boundary, migrated a live purchase system from RevenueCat to StoreKit 2, developed an accessibility and localization workflow, produced App Store assets, launched a privacy-focused website, and built an SEO system whose rankings visibly improved.

More importantly, I learned where an independent developer can hide: inside architecture, polish, metadata, automation, and content volume.

Cold Plunge Timer & Log is live. The engineering is solid. Some keyword rankings are encouraging. The business is not where I wanted it to be.

That is not the ending I would choose for a launch story, but it is the honest one—and probably the more useful story for another iOS developer.
