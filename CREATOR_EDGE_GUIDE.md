# X Algorithm Edge Guide for Creators (IG Models / OnlyFans Influencers)

## Your Unique Advantages in the Algorithm

Based on deep analysis of the X recommendation algorithm, here are **specific edges** for creators driving traffic to external platforms.

---

## 🔥 THE CREATOR-SPECIFIC SIGNALS

### 1. **DM Shares Are Tracked Separately**
```
Signal: share_via_dm_score
Action: ClientTweetClickSendViaDirectMessage
```

**Why This Matters For You:**
- Your audience shares your content privately via DM (not publicly)
- The algorithm **tracks and rewards** DM sharing separately from public reposts
- This is a "private endorsement" signal - high intent engagement

**Edge:** Create content people want to share privately with friends. Suggestive/teasing content gets DM shared more than explicit content that people are embarrassed to share publicly.

---

### 2. **Profile Clicks = Gold**
```
Signal: profile_click_score
Action: ClientTweetClickProfile
```

**Why This Matters For You:**
- Your entire business model is: Tweet → Profile → Link in Bio → Convert
- Every profile click is tracked and weighted
- High profile click rate signals "creator worth following"

**Edge:** Create curiosity gaps. Posts that make people think "who IS this?" drive profile visits. Don't give everything away in the tweet.

---

### 3. **Copy Link Is Tracked**
```
Signal: share_via_copy_link_score
Action: ClientTweetShareViaCopyLink
```

**Why This Matters For You:**
- When fans copy your tweet link to share elsewhere (Discord, Telegram, Reddit)
- This is tracked as positive engagement
- Shows your content has external viral potential

**Edge:** Create screenshot-worthy or share-worthy moments. Content that gets shared to group chats and forums.

---

## 📹 VIDEO STRATEGY

### The MIN_VIDEO_DURATION_MS Threshold

```rust
// Videos ONLY get VQV boost if duration > MIN_VIDEO_DURATION_MS
fn vqv_weight_eligibility(candidate: &PostCandidate) -> f64 {
    if candidate.video_duration_ms.is_some_and(|ms| ms > MIN_VIDEO_DURATION_MS) {
        VQV_WEIGHT  // Gets the boost
    } else {
        0.0  // NO video boost for short clips
    }
}
```

**What This Means:**
- Very short clips (likely <3-5 seconds) get **ZERO** video quality view boost
- The algorithm rewards meaningful video watches, not quick loops

**Edge Strategy:**
| ❌ Avoid | ✅ Do Instead |
|----------|---------------|
| 2-second loop clips | 8-15 second teaser videos |
| GIF-style micro-content | Videos with beginning/middle/end |
| Instant gratification clips | Build-up and payoff structure |

**Optimal Video Formula:**
1. **Hook** (0-2 sec): Attention grab
2. **Build** (2-8 sec): Create anticipation
3. **Payoff** (8-12 sec): Deliver value
4. **CTA** (12-15 sec): Subtle call to action

---

## 📸 PHOTO STRATEGY

### Photo Expand Score
```
Signal: photo_expand_score
Action: ClientTweetPhotoExpand
```

**What Gets Measured:**
- User clicks to expand/view your photo in full
- Indicates the thumbnail created enough interest to click

**Edge Strategy:**
| Technique | Why It Works |
|-----------|--------------|
| Crop strategically | Force expansion to see full image |
| Use portrait orientation | Mobile users must tap to see properly |
| Tease in thumbnail | Create curiosity to see more |
| High quality images | Reward the click with quality |

---

## ⏱️ DWELL TIME EXPLOITATION

### The Hidden Quality Signal
```
Signal: dwell_score + dwell_time (continuous)
Weight: DWELL_WEIGHT + CONT_DWELL_TIME_WEIGHT
```

**What This Means:**
- Algorithm measures how long users look at your tweet
- Longer dwell = higher quality signal
- Both binary (did they dwell?) and continuous (how long?)

**Edge for Creators:**

| Content Type | Dwell Optimization |
|--------------|-------------------|
| **Photos** | Multiple photos in carousel = longer dwell |
| **Text** | Longer captions with story/context |
| **Video** | Engaging content that holds attention |
| **Threads** | Multi-tweet stories keep users engaged |

**Caption Formula:**
```
[Hook line that stops the scroll]

[2-3 lines of context/story]

[Soft CTA or question]
```

---

## 🚫 THE DEADLY MISTAKES

### Negative Signals That DESTROY Your Reach

```rust
// These are SUBTRACTED from your score
- not_interested_score × NOT_INTERESTED_WEIGHT
- block_author_score × BLOCK_AUTHOR_WEIGHT
- mute_author_score × MUTE_AUTHOR_WEIGHT
- report_score × REPORT_WEIGHT
```

**What Triggers These:**

| Signal | Common Triggers for Creators |
|--------|------------------------------|
| **Block** | Aggressive DMs, spam, harassment |
| **Mute** | Posting too frequently, repetitive content |
| **Not Interested** | Content that doesn't match expectations |
| **Report** | TOS violations, explicit content on main feed |

**The Math Problem:**
- One block might negate 10+ likes in the scoring formula
- These signals follow you - they affect ALL your future content
- The model learns "users like this tend to block this creator"

**Edge:** Protect your account reputation aggressively. Never:
- Spam DMs to followers
- Post the same content repeatedly
- Engage with trolls (they'll block you)
- Post content that gets reported

---

## 📊 THE AUTHOR DIVERSITY TAX

### Why Spamming Kills Your Reach

```rust
fn multiplier(&self, position: usize) -> f64 {
    (1.0 - floor) * decay_factor.powf(position as f64) + floor
}
```

**The Penalty Structure:**
| Post # Today | Approximate Reach Multiplier |
|--------------|------------------------------|
| 1st post | 100% |
| 2nd post | ~50% |
| 3rd post | ~25% |
| 4th post | ~12.5% |
| 5th+ post | Near floor (minimal) |

**Edge Strategy:**
- **Quality over quantity** - 2-3 great posts beat 10 mediocre ones
- **Space your posts** - Let the diversity penalty reset
- **Make each post count** - Every post should have a purpose

**Optimal Posting Schedule:**
```
Morning:   1 high-effort post (photo/video)
Afternoon: 1 engagement post (reply to fans, quote tweet)
Evening:   1 teaser/anticipation post
```

---

## 🎯 THE PROFILE CLICK FUNNEL

### Optimizing the Path: Tweet → Profile → Link → Convert

**Step 1: Tweet Creates Curiosity**
```
Goal: Maximize profile_click_score

Tactics:
- Don't show everything in the tweet
- Create "who is this?" moments
- Use captions that imply more content exists
- Mention "link in bio" subtly (not spammy)
```

**Step 2: Profile Delivers**
```
Goal: Convert profile visitor to link clicker

Tactics:
- Pinned tweet with clear value prop
- Bio that explains what they'll get
- Link prominently displayed
- Recent tweets show consistent quality
```

**Step 3: Link Converts**
```
Goal: Turn X traffic into subscribers

Tactics:
- Landing page matches tweet energy
- Clear call to action
- Social proof (subscriber count, testimonials)
```

---

## 🔗 LINK STRATEGY

### The Truth About External Links

**Good News:** External links are NOT penalized by the algorithm
**The Signal:** `share_via_copy_link_score` tracks link sharing positively

**But Watch Out For:**
- Spam filters (VF Filter) can flag suspicious URLs
- Too many link-only posts = low engagement = low reach
- Links reduce native engagement (users leave the platform)

**Edge Strategy:**
| ❌ Avoid | ✅ Do Instead |
|----------|---------------|
| Every tweet has a link | 1 in 5 tweets has direct link |
| "Link in bio" spam | Natural mentions of bio |
| Shortened/suspicious URLs | Clean, recognizable links |
| Link-only tweets | Value-first, link as bonus |

**The 80/20 Rule:**
- 80% of tweets: Pure engagement content (no links)
- 20% of tweets: Promotional with links

---

## 🌐 IN-NETWORK VS OUT-OF-NETWORK

### Understanding Your Two Audiences

**In-Network (Thunder Source):**
- Your existing followers
- See your content with NO penalty
- Ranked by recency
- Reliable, consistent reach

**Out-of-Network (Phoenix Retrieval):**
- Non-followers discovering you
- Your content receives `OON_WEIGHT_FACTOR` penalty (< 1.0)
- ML-matched based on their engagement history
- Growth potential but harder to reach

**Edge Strategy:**

| Audience | Content Strategy |
|----------|------------------|
| **Followers** | Consistent posting, relationship building, direct engagement |
| **Discovery** | Viral-optimized content, trending topics, highly shareable |

**Growth Hack:**
Your followers' engagement (likes, reposts, replies) trains the ML model on who else might like your content. High engagement from followers = better out-of-network discovery.

---

## 💎 THE ULTIMATE CREATOR FORMULA

### Content That Maximizes All Signals

```
OPTIMAL POST =
  High P(repost)      → Shareable, not embarrassing to RT
+ High P(like)        → Visually appealing, positive emotion
+ High P(reply)       → Asks question, invites conversation
+ High P(profile_click) → Creates curiosity about you
+ High P(share_dm)    → Worth sharing privately
+ High P(dwell)       → Takes time to consume
+ High P(follow)      → Signals "more where this came from"
- Low P(block)        → Not annoying or spammy
- Low P(mute)         → Not repetitive
- Low P(report)       → Within TOS
```

### The Perfect Creator Tweet Template

```
[HOOK: Attention-grabbing first line]

[VISUAL: High-quality photo OR 10-15 sec video]

[CONTEXT: 2-3 lines of story/personality]

[ENGAGEMENT: Question or soft CTA]

Posted at: Peak audience hours
Frequency: 2-3x daily max
```

---

## 📈 GROWTH PRIORITY MATRIX

| Priority | Action | Why |
|----------|--------|-----|
| 🔴 Critical | Avoid blocks/mutes/reports | Negative signals destroy reach |
| 🔴 Critical | Don't spam (author diversity) | Exponential penalty per post |
| 🟠 High | Optimize for reposts/quotes | Highest positive weight |
| 🟠 High | Drive profile clicks | Your conversion funnel |
| 🟡 Medium | Create DM-shareable content | Private endorsement signal |
| 🟡 Medium | Maximize dwell time | Quality signal |
| 🟢 Growth | Build genuine follower base | In-network has no penalty |

---

## 🎬 CONTENT IDEAS BY SIGNAL

### Maximize Reposts
- Relatable content your audience wants to share
- Memes related to your niche
- Motivational/aspirational content
- "Tag someone who..." style posts

### Maximize Profile Clicks
- Teaser content implying more exists
- "New content dropping" announcements
- Behind-the-scenes glimpses
- Personality-driven posts

### Maximize DM Shares
- Content fans want to share with friends privately
- "You need to see this" moments
- Exclusive-feeling content
- Inside jokes with your community

### Maximize Dwell Time
- Carousel posts (multiple images)
- Longer captions with stories
- Videos that build anticipation
- Threads with narrative arc

### Maximize Follows
- Showcase your best work
- Demonstrate consistent quality
- Show personality beyond just photos
- Engage with replies (makes you seem accessible)

---

## ⚠️ WHAT THE ALGORITHM DOESN'T CARE ABOUT

Things that **don't directly affect ranking:**

- Hashtags (no special weight found in code)
- Posting time (only affects in-network recency)
- Tweet length (only affects dwell time indirectly)
- Emoji usage (no signal found)
- @mentions (no special weight)

**Focus on engagement signals, not formatting tricks.**

---

## SUMMARY: YOUR COMPETITIVE EDGE

1. **DM shares are your secret weapon** - Create privately shareable content
2. **Profile clicks are everything** - Optimize the curiosity gap
3. **Video must exceed minimum duration** - No lazy 2-second clips
4. **Author diversity kills spam** - Quality over quantity
5. **Negative signals are devastating** - Protect your reputation
6. **Dwell time rewards depth** - Give people reasons to stay
7. **In-network is reliable** - Build genuine followers
8. **The model learns** - Consistent quality trains it to show you to the right people

**Your edge over random users:** You understand the scoring formula. Now optimize for it.
