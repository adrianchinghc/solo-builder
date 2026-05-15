# Platform Policy Risk Register

Reference file for `aso`. Load when writing Component 6 (platform-policy risk register).

> **Policy details change.** Always verify against the current:
> - App Store Review Guidelines: developer.apple.com/app-store/review/guidelines/
> - Google Play Developer Policy Center: play.google.com/about/developer-content-policy/
> 
> The sections below reflect known policy areas as of early 2026. Treat this as a starting checklist, not a substitute for reading current guidelines.

---

## App Store Review Guidelines — hot zones for subscription apps

### 3.1.2 — Subscriptions

**The requirement:** The subscription price, billing period, and free trial terms (if any) must be clearly disclosed to the user before they commit to a subscription.

**Common rejection patterns:**
- Price displayed in small gray text below the subscribe button
- Free trial duration stated in a tooltip or expandable section instead of the primary paywall view
- Annual price shown without the monthly equivalent ("$59.99/year" without "$4.99/month equivalent")
- Subscription terms buried in the Terms of Service link rather than displayed inline

**What compliant looks like:**
- Primary paywall displays: price ($X.XX/month or $X.XX/year), billing period (monthly/annual), free trial duration if applicable ("Try free for 7 days, then $X/month"), and a clear CTA button
- A "Terms of Service" and "Privacy Policy" link is present (required, but separate from the pricing disclosure)

**Apple's specific requirement:** For apps offering auto-renewable subscriptions, the App Store product page and the paywall within the app must both clearly state the subscription terms. Apple reviews both.

---

### 3.1.3 — Acceptable subscription content

**The requirement:** Auto-renewable subscriptions must provide ongoing value — new or updated content, service access, or features — on a recurring basis.

**Risk scenario:** A one-time utility (e.g., a tool that generates a single output, a converter) sold as a monthly subscription may be rejected if Apple determines there's no ongoing value being delivered. The argument "it's software maintenance" is not sufficient.

**Mitigation:** Ensure each billing period genuinely delivers: new content (updated templates, exercises, sounds, data), active server-side features (sync, backup, API access), or a feature roadmap that's being executed. Document this in your App Review notes if the subscription model could be questioned.

---

### 5.1.1(v) — Account sign-up walls

**The requirement:** Apps may not require users to create an account before accessing basic app functionality.

**Common rejection pattern:** Onboarding flow that ends with a required account creation screen before any app feature is accessible. Users must be able to "look around" before committing to an account.

**Compliant design patterns:**
- Allow guest/anonymous access to the core feature, prompt for account creation at a natural save/sync point
- Present account creation as a benefit ("Sign up to save your progress") rather than a gate
- Offer "Continue without account" option on the account creation screen

**Exception:** Apps where the core function is inherently account-based (banking, social network, communication apps) are exempt. "Habit tracker" and most utility apps are NOT exempt.

---

### 5.1.1 — Data collection and privacy

**The requirement:** The Privacy Nutrition Label in App Store Connect must accurately reflect all data types your app collects, how they're linked to user identity, and how they're used for tracking.

**Risks:**
- Under-disclosure: if your app collects data not listed in the nutrition label, rejection and possible removal
- Third-party SDK disclosure: if you include an analytics SDK, crash reporting, or ad SDK, that SDK's data collection must be included in your disclosure even if your own code doesn't collect it. Review each SDK's privacy documentation.

**Practical checklist:**
- [ ] List all first-party data collected (email, name, device ID, usage data)
- [ ] List all third-party SDKs and check their privacy manifests
- [ ] RevenueCat: discloses purchase data, may link to identity (check revenuetcat.com/privacy)
- [ ] Firebase/Crashlytics: discloses crash data and device identifiers
- [ ] Amplitude/PostHog: discloses behavioral analytics data
- [ ] Sentry: discloses crash data and potentially PII in error messages if not scrubbed

---

### 4.0 — Design standards

**The requirement:** Apps must have genuine native value. A web wrapper that just opens a mobile-formatted website will be rejected.

**Risk for subscription apps:** If your app's "native" features are thin and the primary interface is a web view, Apple may reject under 4.0.

**Mitigation:** Ensure core features use native UI components: push notifications (requires APNs integration, not a web notification), biometric auth, offline access, native share sheet, system widgets, or at minimum a fully native navigation and UI layer.

---

### AI-generated content (emerging — verify current policy)

**Current status (verify at developer.apple.com/app-store/review/guidelines/):**

Apple has been updating requirements around AI-generated content. As of 2026, apps that generate user-facing content using AI (text, images, audio, video) may be required to:
- Disclose that content is AI-generated within the app
- Implement safeguards against generating prohibited content categories (CSAM, hate speech, etc.)
- Include a content reporting mechanism

Verify the current guideline before submitting an AI-generation feature. AI policy is evolving rapidly.

---

## Google Play Developer Policy — hot zones for subscription apps

### Subscription and cancellation clarity

**The requirement:** Users must be able to cancel their subscription easily. Google requires:
- A cancellation path accessible within ≤2 taps from inside the app
- Clear subscription management UI (or link to Google Play subscription management)

**Rejection/removal risk:** Apps that bury cancellation or make it deliberately difficult. This is also grounds for Play Store removal after listing (not just on first submission).

**Implementation:** Add a "Manage Subscription" menu item (or equivalent) in your app's account/settings section. Link to `https://play.google.com/store/account/subscriptions` if you want Google to handle the UI:
```kotlin
val intent = Intent(Intent.ACTION_VIEW, 
    Uri.parse("https://play.google.com/store/account/subscriptions"))
startActivity(intent)
```

---

### Deceptive behavior and misleading listings

**The requirement:** Screenshots, descriptions, and promotional materials must accurately represent the app's current state.

**Common policy violations:**
- Screenshots show UI or features that don't exist in the current app version
- Screenshots use competitor app UI
- Description claims features not present in the app
- App name implies false endorsement (e.g., "Official [Brand] App" when it's not)
- Screenshots show AI-generated UI that looks polished when the actual app is different

**Practical rule:** Every screenshot in your Play Store listing must be takeable by downloading the current version of the app. If you can't produce the screenshot from the live app, it shouldn't be in the listing.

---

### Sensitive permissions

**The requirement:** Each sensitive permission requested must have a clear, legitimate justification declared in the Data Safety section, and the permission must be used for the stated purpose.

**High-risk permissions for typical subscription apps:**

| Permission | Risk | Mitigation |
|------------|------|------------|
| ACCESS_FINE_LOCATION | Requires clear justification; "improve user experience" is insufficient | Only request if location is core to the app's primary function |
| READ_CONTACTS | High scrutiny; must demonstrate why your app needs contacts | Avoid unless contacts sync is the product |
| RECORD_AUDIO | High scrutiny | Legitimate for voice note apps, music apps; requires disclosure |
| READ_CALL_LOG | Typically rejected for non-phone-utility apps | Avoid |
| CAMERA | Generally acceptable with clear use case | State use in Data Safety section |
| BACKGROUND_LOCATION | Requires advanced permission dialog; high rejection risk | Only if background location is the core feature |

---

### Data Safety section accuracy

**The requirement:** The Data Safety form in Play Console must accurately reflect what data your app collects, whether it's shared with third parties, and whether it can be deleted.

**Same risk as iOS:** Third-party SDK data collection must be included. Each SDK you integrate should have a "Data Safety" or "Privacy" documentation page — check them all.

**User data deletion:** If you collect any personal data, you must provide a way for users to request deletion. This can be an in-app option or a web form. Google requires you to declare this capability and provide a URL. Set this up before submission.

---

## Pre-submission compliance checklist

Run this checklist before your first submission to each store, and again after any major feature addition.

**Both stores:**
- [ ] Privacy policy is live at a permanent URL, accessible from the store listing and from within the app
- [ ] All data collection declared in iOS Privacy Nutrition Label / Android Data Safety section matches actual app behavior
- [ ] Third-party SDK data practices reviewed and included in declarations
- [ ] Subscription price, billing period, and free trial terms clearly visible before user commits
- [ ] Screenshots match current live app UI (no mockups, no future-state)
- [ ] Age rating correctly set
- [ ] App does not crash on fresh install on a real physical device (test on both iOS and Android)
- [ ] In-app review prompt does not offer incentives for reviews
- [ ] No competitor brand names used as keywords or in deceptive manner

**iOS-specific:**
- [ ] Privacy Nutrition Label completed in App Store Connect
- [ ] If AI-generated content: disclosure mechanism in place, content moderation reviewed
- [ ] Sign-up wall check: users can access basic functionality without creating an account
- [ ] App preview video shows current live UI
- [ ] Promotional text (170 chars, not indexed) reviewed and accurate

**Android-specific:**
- [ ] Data Safety section completed and accurate in Play Console
- [ ] User data deletion mechanism implemented and URL provided to Google
- [ ] "Manage Subscription" or cancellation path accessible in ≤2 taps from within the app
- [ ] Feature graphic (1024×500px) does not include text in outer 80px margin
- [ ] Short Description (80 chars) accurately describes the app

---

## Rejection-recovery playbook

### Day 0 — Rejection received

Read the full rejection message. Apple rejections cite a specific guideline number (e.g., "Guideline 3.1.2 — Business — Payments — Subscriptions"). Google rejections cite a policy section.

**Do not immediately resubmit.** A premature resubmission with the same issue results in a faster second rejection and may flag your app for additional scrutiny.

### Day 1 — Diagnose

Read the full cited guideline section, not just the headline. Apple and Google often add nuance in subsections that isn't obvious from the violation title.

Ask: is this a design fix (paywall layout), a code fix (permission request flow), a metadata fix (privacy declarations), or a policy fix (need to change a feature)?

### Day 1-3 — Fix

Make the minimal change that addresses the specific rejection. Do not bundle unrelated improvements — they can trigger additional review items and extend the review cycle.

For design fixes (paywall clarity, sign-up wall): redesign and rebuild the affected screen, test on a real device, take new screenshots.

For metadata fixes (privacy declarations, incorrect age rating): update in App Store Connect / Play Console, verify the changes save correctly.

### Resubmit with reviewer notes

**iOS:** In App Review Information section, write a clear note:
```
Dear Reviewer,

We received feedback under Guideline [X.X.X]. We have [specific change made] to address 
this: [brief description]. The [feature/flow] now [compliant behavior]. Thank you for your 
guidance.
```

**Android:** No direct reviewer communication channel. Resubmit after fixes are applied.

### Appeal (iOS only)

If you believe the rejection is incorrect after reading the full guideline:
1. Use the "Reply to Reviewer" functionality in App Store Connect — explain your position, cite the specific guideline text that supports your interpretation
2. Be factual and specific; emotional appeals or escalations are counterproductive
3. If resolution doesn't come within 5 business days: submit a formal appeal via the Resolution Center in App Store Connect

Developer Relations (appstoreconnect.apple.com — contact form) is the last resort. Takes 1-2 weeks. Use only for systemic issues or clear policy misapplication.

**Google has no equivalent public appeal path.** If you have a Google Partner or developer relations contact, that's the escalation route. Otherwise, address the rejection and resubmit.

---

## Strategic risk — platform ships native feature

This is the highest-order risk in any category-displacement play, and no amount of ASO preparation prevents it. Both Apple and Google have a history of shipping native OS features that effectively destroy entire app categories.

**Historical examples:**
- QR code scanning (iOS 11 / Android 9) → eliminated QR scanner app category
- Flashlight (iOS 7 / Android 5) → nearly eliminated flashlight app category
- Screen time / parental controls (iOS 12, Android Digital Wellbeing) → severely compressed parental control app revenue
- Health tracking native (Apple Health, Google Fit) → compressed general health tracking apps
- Wallet / NFC payments (Apple Pay, Google Pay) → eliminated many mobile payment apps

**Assessment timing:**
If Apple announces a native equivalent at WWDC (June each year) or Google announces at Google I/O (May each year) or in a quarterly Android OS release, you have a 6-9 month window before the feature is widely deployed. During this window:

1. Evaluate within 2 weeks whether your differentiator survives native competition. Native wins on default status and distribution, not quality — your app needs to be meaningfully better in some dimension the native version doesn't address.
2. If you can survive native competition: double down on differentiation, build the features that native will never ship (too niche, too specific, too privacy-sensitive).
3. If you cannot survive: pivot to a sub-feature or adjacent category before the OS update ships. Don't wait.

**Hedging strategies:**
- Build cross-platform from day 1 (web app + mobile) so your data and users aren't exclusively in the app
- Ensure your value proposition has at least one layer that the OS cannot replicate without privacy concerns (personalization, cloud sync, social features)
- Categories most resilient to native commoditization: those requiring ongoing content, social features, deep personalization, B2B workflows, or integration with third-party data sources
