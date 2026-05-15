# Review Velocity Playbook

Reference file for `aso`. Load when writing Component 4 (review velocity and freshness signals).

---

## Why review velocity matters for ranking

Both the App Store and Google Play use recent review volume, average rating trend, and review recency as ranking inputs. The exact weighting is not published, but the pattern is well-established: a new app with 50 reviews in 30 days ranks above an old app with 5,000 reviews spread over 5 years for certain keyword clusters — particularly long-tail terms where the ranking algorithm has less overall signal.

For the displacement-attack strategy, the implication is significant: in the first 90 days, you can out-review stale incumbents proportionally. An incumbent with 2,000 reviews who gets 5 new reviews per month is losing freshness ground to a new app that gets 50 reviews in month 1.

The ranking advantage from review velocity is widest in the first 90 days. After that, cumulative review count starts to matter more. This is why front-loading review acquisition in the launch window is a priority, not an afterthought.

---

## In-app review API — iOS (SKStoreReviewController)

Apple provides a native review request dialog that apps can trigger programmatically. Apple controls whether the dialog actually shows — it limits to 3 prompts per 365 days per app version. This means you get at most 3 chances per user per year to prompt a review.

**Swift implementation:**
```swift
import StoreKit

// Call at a positive moment — user has just completed a meaningful action
func requestReviewIfAppropriate() {
    guard let scene = UIApplication.shared.connectedScenes
        .first(where: { $0.activationState == .foregroundActive }) as? UIWindowScene else {
        return
    }
    SKStoreReviewController.requestReview(in: scene)
}
```

**When to call this function:**
- After user successfully completes the core JTBD action for the first time (not after onboarding — after the first real use)
- After user returns for their 3rd session within 7 days (proves retention, user has enough experience to review fairly)
- After user achieves a milestone or goal within the app

**When NOT to call this function:**
- On first launch
- During onboarding flow
- After an error, crash, or failed action
- When user is mid-task
- Immediately after purchase (feels transactional)

**Policy note:** The 3-prompts-per-year limit is enforced by iOS, not by your code. Do not attempt to route around this with a custom modal that mimics the system dialog — this violates App Store Review Guidelines 5.6 and risks removal.

---

## In-app review API — Android (Play In-App Review API)

Google provides equivalent functionality via the Play In-App Review API. Google also limits frequency internally, though the specific limits are not published.

**Kotlin implementation:**
```kotlin
import com.google.android.play.core.review.ReviewManagerFactory
import com.google.android.play.core.review.model.ReviewInfo

class ReviewHelper(private val activity: Activity) {

    fun requestReview() {
        val manager = ReviewManagerFactory.create(activity)
        
        manager.requestReviewFlow()
            .addOnCompleteListener { request ->
                if (request.isSuccessful) {
                    val reviewInfo: ReviewInfo = request.result
                    manager.launchReviewFlow(activity, reviewInfo)
                        .addOnCompleteListener {
                            // Flow complete — do not assume the user left a review
                            // Google does not tell you whether a review was submitted
                        }
                }
            }
    }
}
```

**React Native (Expo) — using `expo-store-review`:**
```typescript
import * as StoreReview from 'expo-store-review';

async function requestReview() {
  const isAvailable = await StoreReview.isAvailableAsync();
  if (isAvailable) {
    await StoreReview.requestReview();
  }
}
```

**Same timing rules apply** as iOS — trigger on positive moments, never during friction.

---

## Timing strategy — positive-moment detection

The most important implementation decision is WHEN to trigger the review prompt. A review prompt at the wrong moment produces 1-star reviews. A review prompt at the right moment produces 5-star reviews from your happiest users.

**High-signal positive moments (customize to your app's core loop):**

| App type | Positive moment to trigger on |
|----------|------------------------------|
| Habit tracker | After user completes a 7-day streak for the first time |
| Expense tracker | After user logs their 10th transaction OR after first month summary is generated |
| Meditation app | After user completes their 5th session |
| Language learning | After user passes a level or completes a lesson module |
| Fitness tracker | After user logs their first completed workout |
| Sleep sounds | After user has used the app for 3 consecutive nights |
| General utility | After user completes the core action 3 times (showing they actually use it) |

**Detection pattern:**
Track a "positive moment reached" flag in local storage (or your backend). Trigger once per event type. Do not re-trigger the same positive moment repeatedly.

```typescript
// Example pattern (React Native / AsyncStorage)
import AsyncStorage from '@react-native-async-storage/async-storage';
import * as StoreReview from 'expo-store-review';

async function checkAndRequestReview(eventKey: string) {
  const alreadyPrompted = await AsyncStorage.getItem(`review_prompted_${eventKey}`);
  if (alreadyPrompted) return;
  
  const isAvailable = await StoreReview.isAvailableAsync();
  if (isAvailable) {
    await StoreReview.requestReview();
    await AsyncStorage.setItem(`review_prompted_${eventKey}`, 'true');
  }
}

// Call after 7-day streak
await checkAndRequestReview('streak_7_days');
```

---

## Review reply strategy

**Reply to every review in the first 60 days.** After 60 days, reply to negative reviews and any review with a specific feature request or bug report.

Why this matters:
- Review replies are visible on the listing — prospective users read them
- Review reply text is indexed by some ASO tools — use keywords naturally without stuffing
- A developer who replies to negative reviews signals trustworthiness; this improves conversion rate
- Apple and Google can see that you're actively managing your app

**Template — positive review (3-5 stars):**
```
Thank you for the review! Really glad [specific thing they mentioned or inferred from rating] 
is working well for your [use case]. If you have friends dealing with [problem statement], 
we'd love if you shared [App Name]. — [Your name/team]
```

Customize per review. Do not paste the same template verbatim on every review — both platforms can detect this, and users can see it.

**Template — negative review (1-2 stars with specific complaint):**
```
We're sorry [issue they mentioned] got in the way. This is directly on our fix list — 
[specific what you're doing about it if applicable]. Please reach out at [support email] 
and we'll make it right. Your feedback shapes what we fix next. — [Your name]
```

**Template — negative review (1-2 stars without specific complaint):**
```
Thanks for taking the time to review. We'd genuinely like to understand what went wrong — 
would you mind reaching out at [support email]? We read every message and take them 
seriously. — [Your name]
```

**What not to do:**
- Do not argue with negative reviewers publicly
- Do not ask reviewers to change their review (violates platform policy)
- Do not offer compensation in exchange for review changes (violates policy)

---

## Policy line — review incentivization (FORBIDDEN)

Neither Apple nor Google permits offering any reward in exchange for reviews or for changing a review rating. Specifically forbidden:

- Offering discount codes, in-app currency, free premium features, or any other benefit in exchange for leaving a review
- Offering rewards for leaving a 5-star review specifically (as opposed to any review)
- Running contests or sweepstakes where entering requires leaving a review
- Asking users to change their review in exchange for resolving their issue

**Legitimate:** Asking sincerely at a positive moment in the user experience. "We'd love to hear your feedback" or "If you're enjoying the app, a review helps us a lot" — with no reward attached.

Violations can result in:
- App removal from the store
- Developer account suspension
- Review removal by the platform

---

## Update cadence as freshness signal

Shipping updates is the single highest-leverage ASO action available to a new app in the first 6 months. Every meaningful update:

1. **Resets the "Updated" date** on your store listing — this is visible to users; stale incumbents show "Updated 3 years ago" while yours shows "Updated 2 days ago"
2. **Triggers What's New text** — keyword-rich opportunity that the algorithm reads
3. **Re-indexes your keyword field (iOS)** — allows you to respond to keyword performance data
4. **Signals to the algorithm** that the app is actively maintained, correlating with lower churn

**Target cadence:** One meaningful update every 2-3 weeks for the first 6 months.

**What counts as "meaningful":**
- New user-visible feature
- Significant UX improvement or redesign of a major flow
- New language localization
- Significant performance improvement (measured, not estimated)

**What does NOT count:**
- Version bump with "bug fixes" only
- Backend-only changes with no user-visible effect
- Icon or color changes as a "launch"
- Dependency updates invisible to users

**Writing "What's New" text:**
Write as a mini-pitch, not a changelog. Lead with user benefit, include keywords naturally, mention a specific user segment if applicable.

Good example (habit tracker update):
```
v2.3: Shift workers, this one's for you — you can now set rotating schedules so your 
habits adapt when you switch from days to nights. Plus: streak recovery for planned 
days off (life happens), and faster load times across the board.
```

Bad example:
```
v2.3: Bug fixes and performance improvements. Fixed crash on iOS 17.4. Updated 
dependencies.
```

The bad version is accurate but invisible to the ranking algorithm and users.

---

## Crash-free rate and retention as indirect signals

**Crash-free rate:**
- Both platforms monitor crash rates. A high crash rate (>1%) correlates with:
  - Lower user satisfaction (more 1-star reviews)
  - Reduced algorithm-promoted placement on "Featured" and algorithmic recommendations
  - Potential "Low Quality" flags in App Store Connect
- Target: ≥99.5% crash-free rate
- Tool: Firebase Crashlytics (free tier, generous limits) — integrate in the first build, not after launch
- Expo: `npx expo install expo-firebase-analytics` + `@react-native-firebase/crashlytics`
- Sentry: `npx expo install sentry-expo` — alternative with free hobby tier

**Retention targets:**
Algorithm inputs for both platforms include retention signals (exact mechanisms not published, but correlated with ranking).
- D1 retention target: ≥40% (40% of day-1 users return on day 2)
- D7 retention target: ≥20% (20% of day-1 users still active on day 7)
- D30 retention target: ≥10%

These targets are benchmarks for average-quality apps. Exceeding them correlates with stronger algorithmic placement.

Measure retention with:
- RevenueCat (if subscription app) — tracks active subscriber retention
- Amplitude Mobile (free tier) — cohort retention analysis
- PostHog (free tier for low volume) — custom retention funnels
- Firebase Analytics (free) — basic retention cohorts without third-party dependency
