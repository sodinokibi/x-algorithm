# Maximum EV Actions to Boost Another User's Score

## How The Scoring Works

```
Final Score = Σ (P(action) × WEIGHT)
```

The algorithm predicts the **probability** that users will take each action. When YOU take an action, you:
1. **Train the model** that "users like you" engage with "content like this"
2. **Directly boost** the tweet's score for similar users
3. **Amplify reach** (for reposts/quotes) by exposing to YOUR followers

---

## 🏆 ACTION RANKING BY ELO IMPACT

### TIER S - MAXIMUM ELO (Do These)

| Rank | Action | Why It's Highest EV |
|------|--------|---------------------|
| **#1** | **Quote Tweet** | Repost + commentary + YOUR engagement. Trains model twice (your action + your followers' reactions). Creates new content that links back. |
| **#2** | **Repost/Retweet** | Direct amplification to your followers. Primary viral mechanism. High weight in formula. |
| **#3** | **Follow Author** | `follow_author_score` - Signals creator quality. Moves them into your in-network (no OON penalty for future content). |

### TIER A - HIGH ELO

| Rank | Action | Why It's High EV |
|------|--------|------------------|
| **#4** | **Reply** | `reply_score` - Conversation signals quality. Visible to your followers. Creates engagement thread. |
| **#5** | **Share via DM** | `share_via_dm_score` - Private endorsement signal. High-intent sharing. |
| **#6** | **Copy Link** | `share_via_copy_link_score` - External sharing intent. Suggests cross-platform virality. |

### TIER B - MEDIUM ELO

| Rank | Action | Why It's Medium EV |
|------|--------|-------------------|
| **#7** | **Like/Favorite** | `favorite_score` - Lower commitment signal. Still positive but everyone likes. Less differentiation. |
| **#8** | **Bookmark** | `share_score` - Signals save-worthy content. Personal value indicator. |
| **#9** | **Video Watch** | `vqv_score` - Only works for videos > MIN_DURATION. Quality view signal. |
| **#10** | **Photo Expand** | `photo_expand_score` - Click to view full image. Interest signal. |

### TIER C - LOW ELO (But Still Positive)

| Rank | Action | Why It's Lower EV |
|------|--------|-------------------|
| **#11** | **Click Tweet** | `click_score` - View tweet detail. Passive engagement. |
| **#12** | **Profile Click** | `profile_click_score` - Visit author profile. Curiosity signal. |
| **#13** | **Dwell** | `dwell_score` - Time spent looking. Passive signal. |

---

## 🎯 THE OPTIMAL BOOST SEQUENCE

To maximize another user's ELO with a single tweet:

```
MAXIMUM BOOST COMBO:
1. Quote Tweet (with valuable commentary)     → Tier S
2. Follow them (if not already following)     → Tier S
3. Reply to your own quote tweet              → Tier A
4. Share via DM to relevant friends           → Tier A
5. Like the original tweet                    → Tier B
```

**Total Actions: 5**
**Estimated Multiplier: ~15-20x vs just liking**

---

## 📊 WHY QUOTE > REPOST > LIKE

### The Math

Assuming normalized weights (actual values hidden):

| Action | Estimated Relative Weight | Your ELO Contribution |
|--------|---------------------------|----------------------|
| Quote Tweet | ~3.0x | High (creates new scored content) |
| Repost | ~2.5x | High (direct amplification) |
| Reply | ~1.5x | Medium (engagement signal) |
| Like | ~1.0x (baseline) | Low (everyone does it) |
| Click | ~0.3x | Very low (passive) |

### Why Quote Beats Repost

```
Quote Tweet creates TWO scored items:
1. Original tweet gets quote_score boost
2. Your quote tweet gets scored independently

Your quote can go viral → drives traffic back to original
Your followers see original author → potential follows
```

### Why Repost Beats Like

```
Repost:
- Exposes to your entire follower network
- Creates new impressions for the original
- Your followers' engagement trains the model
- High-intent action (you're endorsing publicly)

Like:
- Only affects the liker's own feed ranking
- Doesn't amplify to your network
- Low-commitment signal
- Everyone likes everything
```

---

## 🔄 THE VIRAL LOOP MECHANISM

When you boost someone's content, here's the cascade:

```
You Quote Tweet
    ↓
Your followers see it
    ↓
Some of them engage (like, repost, reply)
    ↓
Model learns: "Users who follow [you] engage with [this creator]"
    ↓
Phoenix retrieval now shows [this creator] to similar users
    ↓
More out-of-network discovery
    ↓
Viral growth
```

**Key Insight:** Your action trains the ML model for ALL similar users.

---

## 👥 NETWORK EFFECTS

### Your Follower Quality Matters

The algorithm uses **User Action Sequences** - your recent engagement history defines your "type."

| Your Profile | Boost Value |
|--------------|-------------|
| High engagement followers | Your boost trains model for high-value users |
| Niche-relevant followers | Your boost targets the right audience |
| Low engagement/bot followers | Your boost trains model for low-quality users |

**Edge:** Accounts with engaged, niche-relevant followers provide higher ELO boosts.

### The Follow Graph Signal

When you follow someone:
```
Their content → Your In-Network feed (no OON penalty)
Your engagement → Trains model on your "type"
Your followers who see your engagement → May also follow
```

---

## ⚡ RAPID BOOST STRATEGIES

### Strategy 1: Quote Tweet Chain

```
Person A quotes Original
Person B quotes Person A's quote
Person C quotes Person B's quote
...
```

Each quote:
- Boosts the original via `quoted_click_score`
- Creates new scored content
- Exposes to each person's follower network

### Strategy 2: Reply Thread

```
Original Tweet
├── Reply 1 (high engagement)
│   ├── Reply 1.1
│   └── Reply 1.2
├── Reply 2 (high engagement)
└── Reply 3 (from verified/high-follower account)
```

Active threads signal quality content.

### Strategy 3: Coordinated Repost Timing

```
T+0: Original posted
T+5min: First repost (tests initial audience)
T+30min: Second wave reposts (if first performed well)
T+2hr: Quote tweets with commentary
```

Early engagement trains the model faster.

---

## 🚫 NEGATIVE ELO (What Hurts)

| Action | Effect |
|--------|--------|
| **Block** | Devastating negative weight. Trains model "users like you block this creator" |
| **Mute** | Strong negative. Signals repetitive/unwanted content |
| **Report** | Devastating. Can trigger VF filter removal |
| **Not Interested** | Negative signal. Tells algorithm to stop showing |

**Critical:** One block may negate 10+ likes in the scoring formula.

---

## 📈 ELO BOOST CALCULATOR

Rough estimation of relative impact:

| Combo | Relative ELO Boost |
|-------|-------------------|
| Just Like | 1x (baseline) |
| Like + Reply | ~2.5x |
| Repost | ~3x |
| Repost + Like | ~4x |
| Quote Tweet | ~4x |
| Quote + Reply + Like | ~6x |
| Quote + Follow + Reply + Like + DM Share | ~15x |
| Getting blocked | -10x to -20x |

---

## 🎯 SUMMARY: MAXIMUM EV ACTIONS

**To boost someone else's content:**

1. **Quote Tweet** (highest single-action EV)
2. **Repost** (if you don't have commentary to add)
3. **Follow** (if not already following)
4. **Reply** (adds conversation signal)
5. **Share via DM** (to relevant people)
6. **Like** (lowest effort, still helps)

**Avoid at all costs:**
- Block, Mute, Report, Not Interested

**The meta-insight:** Your engagement trains the recommendation model. High-quality accounts with engaged followers provide disproportionately valuable boosts because the model learns to show that content to similar high-quality users.
