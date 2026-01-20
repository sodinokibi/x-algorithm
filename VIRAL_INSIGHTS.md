# X (Twitter) Algorithm Analysis: How to Go Viral

## Executive Summary

The X recommendation algorithm is a sophisticated multi-stage ML pipeline that combines **in-network content** (from accounts you follow) with **out-of-network content** (discovered via ML). The core ranking uses a **Grok-based transformer model** that predicts 18 different engagement types to score each tweet.

---

## How the Algorithm Works (Simplified)

```
┌─────────────────────────────────────────────────────────────────┐
│                     FOR YOU FEED PIPELINE                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. CANDIDATE SOURCING (parallel)                               │
│     ├── Thunder (In-Network): Recent posts from followed users  │
│     └── Phoenix (Out-of-Network): ML retrieval from all posts   │
│                                                                  │
│  2. FILTERING (10 filters)                                      │
│     Remove: duplicates, old posts, blocked/muted authors,       │
│             muted keywords, previously seen, own posts          │
│                                                                  │
│  3. ML SCORING (Grok Transformer)                               │
│     Predict: P(like), P(reply), P(repost), P(share), etc.      │
│                                                                  │
│  4. WEIGHTED COMBINATION                                        │
│     Score = Σ(weight × P(engagement)) - negative_signals        │
│                                                                  │
│  5. DIVERSITY & RANKING                                         │
│     Apply author diversity, bias toward in-network              │
│                                                                  │
│  6. SERVE TOP K RESULTS                                         │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## The 18 Engagement Signals That Determine Your Reach

### Positive Signals (Higher = More Reach)

| Signal | Description | Viral Impact |
|--------|-------------|--------------|
| **Retweet/Repost** | User reposts your tweet | 🔥🔥🔥 Highest |
| **Like/Favorite** | User likes your tweet | 🔥🔥🔥 High |
| **Reply** | User replies to your tweet | 🔥🔥 High |
| **Quote Tweet** | User quotes your tweet | 🔥🔥🔥 Highest |
| **Share via DM** | User shares in direct messages | 🔥🔥 High |
| **Copy Link** | User copies tweet link | 🔥🔥 High |
| **Click** | User clicks to view full tweet | 🔥 Medium |
| **Profile Click** | User visits your profile | 🔥 Medium |
| **Video Quality View** | User watches video meaningfully | 🔥🔥 High (for videos) |
| **Photo Expand** | User expands your photo | 🔥 Medium |
| **Dwell Time** | How long user reads your tweet | 🔥🔥 High |
| **Follow Author** | User follows you after seeing tweet | 🔥🔥🔥 Highest |

### Negative Signals (Kills Your Reach)

| Signal | Description | Impact |
|--------|-------------|--------|
| **Not Interested** | User clicks "not interested" | ❌❌ Very Bad |
| **Block Author** | User blocks you | ❌❌❌ Devastating |
| **Mute Author** | User mutes you | ❌❌ Very Bad |
| **Report** | User reports your tweet | ❌❌❌ Devastating |

---

## Key Insights for Going Viral

### 1. **Engagement Velocity Matters**
The algorithm uses your **recent engagement history** (User Action Sequence) to predict what you'll engage with. Posts that get quick initial engagement signal quality to the model.

**Actionable**: Post when your audience is active. Get engagement in the first hour.

### 2. **Reposts/Quote Tweets Are King**
Reposts are the strongest viral signal. The algorithm specifically predicts `retweet_score` and `quote_score` with high weight.

**Actionable**: Create content that people want to share with their followers. Ask yourself: "Would someone repost this to their timeline?"

### 3. **The Two-Tower Discovery System**
Out-of-network reach (reaching people who don't follow you) uses a **two-tower embedding model**:
- Your tweet is encoded into an embedding
- Users are encoded based on their engagement history
- Similar embeddings = your tweet gets shown to that user

**Actionable**: Create content similar to high-engagement tweets in your niche. The model learns patterns.

### 4. **Author Diversity Dampening**
The algorithm applies **exponential decay** to multiple posts from the same author:
```
1st post: 100% score
2nd post: ~50% score
3rd post: ~25% score
```

**Actionable**: Don't spam. Quality over quantity. Space out your posts.

### 5. **In-Network Bias**
Out-of-network posts receive a **penalty multiplier** (e.g., 0.7-0.9x score). Content from followed accounts is prioritized.

**Actionable**: Build genuine followers. Your content reaches followers more reliably than strangers.

### 6. **Negative Signals Are Devastating**
Blocks, mutes, and "not interested" clicks heavily penalize your content. The weighted scorer **subtracts** these probabilities.

**Actionable**: Never post content that makes people want to block/mute you. Controversy ≠ engagement if it causes blocks.

### 7. **Dwell Time Is Tracked**
The model predicts `dwell_time` - how long users will read your tweet. Longer dwell = higher quality signal.

**Actionable**: Write tweets worth reading. Hooks that deliver value. Threads for complex topics.

### 8. **Video Duration Matters**
Video posts have special handling - `vqv_score` (video quality view) only counts if the video exceeds `MIN_VIDEO_DURATION_MS`.

**Actionable**: Short videos that are immediately engaging. Don't make 2-second clips expecting video boost.

### 9. **Freshness Matters for In-Network**
The Thunder source (in-network) ranks by **recency**. Newer posts surface first to followers.

**Actionable**: Timing matters for reaching your followers. Post when they're online.

### 10. **There Are No Hand-Engineered Features**
The Grok transformer learns everything from raw engagement data. No magic hashtag tricks, no keyword stuffing.

**Actionable**: Focus on genuine engagement, not gaming tactics. The model adapts.

---

## What the Algorithm Filters Out

Your tweet will be **removed from consideration** if:

1. **Too Old**: Exceeds `MAX_POST_AGE` threshold (typically ~30 days)
2. **Contains Muted Keywords**: User has muted words in your tweet
3. **From Blocked/Muted Author**: User blocked or muted you
4. **Previously Seen**: Already shown to this user
5. **Duplicate Content**: Same tweet/retweet already in feed
6. **Failed Quality Check**: Spam, deleted, policy violation
7. **Paywalled**: User can't access subscription content

---

## The Viral Content Formula

Based on the algorithm's design:

```
Viral Score =
    HIGH: P(repost) × repost_weight
  + HIGH: P(like) × like_weight
  + HIGH: P(quote) × quote_weight
  + HIGH: P(reply) × reply_weight
  + MED:  P(share) × share_weight
  + MED:  P(dwell) × dwell_weight
  + MED:  P(follow) × follow_weight
  - LOW:  P(block) × block_weight
  - LOW:  P(mute) × mute_weight
  - LOW:  P(report) × report_weight
```

**Maximize**: Repostable, likeable, quotable, conversation-starting content
**Minimize**: Content that gets you blocked, muted, or reported

---

## Technical Architecture Summary

| Component | Technology | Purpose |
|-----------|------------|---------|
| Home Mixer | Rust/gRPC | Orchestrates the pipeline |
| Thunder | Rust | In-network post retrieval |
| Phoenix | Python/JAX | ML models (ranking + retrieval) |
| Grok | Transformer | Engagement prediction |
| Strato | Database | User features & caching |

### Key Files in Codebase

- `phoenix/recsys_model.py` - The Grok ranking model
- `phoenix/recsys_retrieval_model.py` - Two-tower discovery model
- `home-mixer/scorers/weighted_scorer.rs` - Engagement weighting
- `home-mixer/scorers/author_diversity_scorer.rs` - Prevents author spam
- `home-mixer/filters/` - All 10 filtering mechanisms

---

## Summary: The Science of X Virality

1. **The algorithm is personalized** - What works for one audience may not work for another
2. **Engagement predicts engagement** - The model learns from patterns of high-engagement content
3. **Negative signals hurt more than positive signals help** - Avoid content that causes blocks/mutes
4. **Quality beats quantity** - Author diversity dampening penalizes spam
5. **In-network is easier than out-of-network** - Building followers is the sustainable path
6. **The model adapts** - No static "hacks" will work long-term; focus on genuine value

**Bottom line**: Create content that your target audience genuinely wants to repost, like, quote, and discuss - while avoiding content that makes them want to block or mute you.
