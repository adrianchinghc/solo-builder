# Listing Asset Specifications

Reference file for `aso`. Load when writing Components 2 and 3 (listing optimization + visual assets).

> **IMPORTANT:** Platform specifications change with OS and developer tool updates. Always verify current dimensions and requirements against:
> - Apple: developer.apple.com/app-store/product-page/ and App Store Connect Help
> - Google: support.google.com/googleplay/android-developer/ and Play Console Help
> 
> The specs below were current as of early 2026. Verify before producing final assets.

---

## iOS — App Store metadata fields

| Field | Limit | Indexed for search? | Notes |
|-------|-------|-------------------|-------|
| App Name | 30 chars | Yes | Primary keyword must appear here |
| Subtitle | 30 chars | Yes | Secondary keyword; don't repeat terms from Name |
| Promotional Text | 170 chars | No | Conversion copy; updatable without App Review |
| Description | 4,000 chars | No | Conversion copy only; not indexed by App Store search |
| Keyword Field | 100 chars | Yes | Comma-separated, no spaces after commas, no words already in Name/Subtitle |

---

## iOS — Visual assets

| Asset | Dimensions | Format | Notes |
|-------|-----------|--------|-------|
| App Icon | 1024×1024px | PNG, no alpha channel, no transparency | OS applies rounded corner mask; don't pre-round |
| iPhone 6.7" screenshots | 1290×2796px or 1320×2868px | PNG or JPEG | Required; verify exact required sizes in App Store Connect (Apple updates annually) |
| iPhone 6.5" screenshots | 1242×2688px or 1284×2778px | PNG or JPEG | Can auto-generate from 6.7" screenshots in ASC |
| iPhone 5.5" screenshots | 1242×2208px | PNG or JPEG | Older device size; some markets still require |
| iPad 12.9" screenshots | 2048×2732px | PNG or JPEG | Required if app supports iPad |
| iPad 11" / 10.5" screenshots | 1668×2388px / 1668×2224px | PNG or JPEG | May auto-generate from 12.9" |
| App preview video | Match screenshot dimensions for device size | H.264 or HEVC, up to 500MB, 15-30s | Autoplay muted in search results; captions essential |

**Screenshot counts:**
- Minimum 1, maximum 10 per device size
- First 3 screenshots display in search results without user expanding — these do 90%+ of conversion work

**Screenshot orientation:**
- Portrait screenshots display in portrait; landscape in landscape
- For games or apps with landscape UI, submit landscape screenshots
- Mixed orientation allowed within a single listing

---

## Google Play — metadata fields

| Field | Limit | Indexed for search? | Notes |
|-------|-------|-------------------|-------|
| App Title | 30 chars | Yes | Primary keyword must appear here |
| Short Description | 80 chars | Yes | Punchline + secondary keyword |
| Full Description | 4,000 chars | Yes (NLP-indexed) | Write naturally; include keyword clusters throughout |

---

## Google Play — visual assets

| Asset | Dimensions | Format | Notes |
|-------|-----------|--------|-------|
| App Icon | 512×512px | PNG, 32-bit with alpha | |
| Feature Graphic | 1024×500px | JPG or 24-bit PNG | Required to be featured; text must stay 80px inside edges on all sides |
| Phone screenshots | Min 320px, max 3840px on any side; aspect ratio 16:9 to 9:16 | PNG or JPEG | Min 2, max 8 |
| 7-inch tablet screenshots | Same dimension constraints as phone | PNG or JPEG | Optional but recommended |
| 10-inch tablet screenshots | Same dimension constraints as phone | PNG or JPEG | Optional but recommended |
| Promo video | YouTube URL (unlisted or public) | YouTube video | Autoplay in listing; 30s-2min optimal; must be accessible without login |

---

## Screenshot narrative structure

**The rule of three:** First 3 screenshots do 90%+ of conversion. Design these first, test these first, and never publish without these optimized.

**Screenshot 1 — Core value statement:**
- Purpose: Answer "what is this app and why should I download it?" in 3 seconds at thumbnail size
- Elements: Bold headline overlay (primary benefit in user's language, not app feature language) + clean UI showing the core feature in active use
- What NOT to include: app name (it's already in the listing title), marketing adjectives ("amazing," "powerful"), company logo, decorative gradients with no content, the splash/loading screen
- Thumbnail test: shrink to 100px wide. Is the core value legible? If not, redesign.

**Screenshot 2 — Problem → solution contrast:**
- Purpose: Create emotional resonance by showing the before (frustration, manual work, broken state) and after (relief, automation, resolved)
- Layout options: side-by-side comparison, before/after scroll, or "without [app] vs. with [app]" narrative
- Headline: should name the problem AND the resolution in one line (e.g., "Stop counting macros manually. Just scan.")

**Screenshot 3 — Social proof injection:**
- Purpose: Provide third-party validation before the user decides to install
- Options (in order of strength): real review quote (with permission or paraphrased accurately), meaningful metric ("50,000 users tracking daily" — when true), award or press mention, App Store feature badge
- Do not fabricate metrics or pull reviews out of context. Placeholder: leave this screenshot for after you have real proof; ship with 2 screenshots if necessary.

**Screenshots 4-10 — Feature highlights:**
- Each screenshot should highlight one feature or user segment
- Follow same structure: headline overlay + UI in use
- Maintain visual consistency: same device frame, same font treatment, same brand palette

---

## App preview video structure

**Optimal length:** 15-30 seconds. Longer videos lose most viewers by second 10.

**Structure:**
| Seconds | Content | Notes |
|---------|---------|-------|
| 0-3 | Hook — the gotcha moment | The most surprising or immediately compelling thing the app does. Must work muted with captions. Must stop the scroll. |
| 4-15 | Core value demo | Live UI walkthrough — show the app actually working on a real task, not a slideshow of features |
| 16-25 | Secondary value or social proof | Supporting feature or a review quote overlaid on UI |
| 25-30 | CTA frame | "Download free" or "Try 7 days free" + price if paid. Show store badge or app icon. |

**Production requirements:**
- Caption all text — the majority of app preview views in search results are muted (autoplay with sound off)
- Record on a real device, not a simulator — UI animations and transitions look different in production
- Use device frames (available from Apple Design Resources at developer.apple.com/design/resources/) for a polished appearance without heavy production budget
- Background music is permitted but cannot be the primary information carrier — all key messages must be visible in captions

---

## Feature graphic (Android only)

**Specifications:** 1024×500px, JPG or 24-bit PNG.

**Critical:** Keep all text and key visuals in the inner 80% of the image (i.e., 80px clear border on all sides). On many Android devices and form factors, the outer edges are cropped when the feature graphic is displayed. Text in the margin zone will be invisible to some users.

**What works:** Simple, bold typography stating the core benefit + complementary UI screenshot or abstract graphic. Brand color as background.

**What doesn't work:** Repeating the app icon in the feature graphic (the icon is displayed separately and adjacent — don't waste the real estate). Screenshot-only without any text overlay (misses the opportunity to state value). Heavy gradients with low-contrast text (accessibility issue + policy risk).

---

## Asset production for solo builders

**Figma resources (free):**
- Search "App Store screenshots template" in Figma Community — multiple high-quality templates for iOS and Android with correct dimensions and device frame overlays
- Apple Design Resources at developer.apple.com/design/resources/ — official device frames, SF Symbols, system UI elements

**Video editing:**
- DaVinci Resolve (free) — capable of producing professional app preview videos
- CapCut (free) — faster for simple screen recording + caption + music workflows
- Rotato (paid, ~$50) — high-quality 3D device frame animations; produces the kind of video that looks professional without a video production background

**Screenshot automation:**
- fastlane/snapshot (free, open source) — automates screenshot capture across device sizes using the iOS Simulator; eliminates manual screenshot taking per device size
- Fastlane frameit — automatically adds device frames to screenshots

**App preview video recording:**
- iOS: QuickTime Player connected to iPhone → File → New Movie Recording → select iPhone as camera. Records at full resolution.
- Android: `adb shell screenrecord /sdcard/demo.mp4` — records device screen at device resolution
