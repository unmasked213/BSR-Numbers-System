# BSR Algorithm for Humans
## A Simple, Non-Technical Explanation

**What This System Does:**
Takes a list of repeated numbers you saw during the day and picks 5 or 6 final numbers from them using specific pattern rules.

---

## The Big Picture

Imagine you keep seeing certain numbers throughout your day: on clocks (14:41), receipts, license plates, etc. You write them all down:

**Your List:**
- 1441
- 1707
- 2323
- 1155
- 0404
- 5050

**What the System Does:**
It analyzes these numbers, finds patterns, creates possible choices, and then picks the 5 or 6 "best" numbers based on rules.

**Final Result:**
- **Chosen Numbers:** 5, 14, 23, 35, 47, 50
- **Balance:** 1 low, 2 medium, 3 high (explained below)

---

## How It Works: 7 Simple Steps

### Step 1: Clean Up Your Numbers

First, the system makes sure all your numbers are valid:
- Removes spaces and dashes (0 0 0 4 → 0004)
- Checks each number is "real" (exists in a reference list)
- Needs at least 2 digits per number

**Example:**
- "14-41" becomes "1441" ✓
- "1.7.0.7" becomes "1707" ✓
- "9" is too short ✗

---

### Step 2: Group Numbers into "Constellations"

Your numbers get divided into small groups of 2-3 numbers each. Think of these like study groups.

**Why?** The system looks for patterns that show up across multiple groups. If a number appears in several groups, it's more likely to be chosen.

**Example with 6 numbers:**
- Group 1: [1441, 1707, 2323]
- Group 2: [1155, 0404, 5050]

**Example with 10 numbers:**
- Group 1: [1441, 1707, 2323]
- Group 2: [1155, 0404, 5050]
- Group 3: [1234, 1111]
- Group 4: [2222, 3333]

---

### Step 3: Find Patterns and Extract Numbers

For each group, the system looks for special patterns and extracts smaller numbers from the big numbers.

#### What Gets Extracted?

**From every number:**
1. **2-digit chunks:** 1441 → 14, 44, 41
2. **Individual digits:** 1441 → 1, 4, 4, 1
3. **Digit sums:** 1441 → 1+4+4+1 = 10

#### Special Patterns Give Bonus Numbers:

**1. Portal (if there's a 0):**
   - Any number with a 0 adds "50" as a choice
   - Example: 1707 contains 0 → adds 50

**2. Mirror (if digits flip):**
   - 1441 has 14 and 41 (mirror pairs)
   - Also has 44 (middle digits match)

**3. Twins (repeated digits):**
   - 2255 has 22 and 55
   - Also adds sums: 2+2=4, 5+5=10
   - And products: 2×2=4, 5×5=25

**4. Palindrome (reads same forward/backward):**
   - 1441 is a palindrome
   - Extracts all chunks: 14, 44, 41
   - And the total sum: 10

**5. ABAB pattern (repeating blocks):**
   - 2323 repeats "23"
   - Extracts: 23, 32 (reverse), 5 (2+3), 10 (total)

**Result of Step 3:**
Each group now has a "pool" of 10-30 smaller numbers to work with.

**Example Pool from 1441:**
- {1, 4, 10, 14, 41, 44}

---

### Step 4: Create More Options Through Math

Now the system combines the pool numbers using simple math to create more choices.

**Rules:**
- **Direct:** Any number already in the pool (no math needed)
- **1-step math:** Add, subtract, multiply, or divide pool numbers once
  - Example: 14 + 1 = 15
  - Example: 44 - 1 = 43
  - Example: 5 × 7 = 35
- **2-step math:** Do two operations in sequence
  - Example: (14 + 1) + 10 = 25

**Important Limits:**
- Subtraction: always bigger minus smaller (14 - 1, not 1 - 14)
- Division: only if it makes a whole number (15 ÷ 3 = 5 ✓, but 15 ÷ 4 = 3.75 ✗)
- No crazy math: no powers, no square roots, no decimals
- Final numbers must be in range (1-59 or 1-50 depending on mode)

**What This Step Produces:**
Each group now has 50-200 possible candidate numbers, each with a "recipe" showing how it was made.

---

### Step 5: Find Numbers That Appear Everywhere ("Convergence")

Here's the key: **Numbers that show up in multiple groups are more likely to be chosen.**

**The Rule:**
A number needs to appear in at least **70% of the groups** to be considered good.

**Example:**
- You have 5 groups total
- 70% of 5 = 3.5, rounded up = 4 groups
- So a number must appear in at least 4 groups

**Why This Matters:**
If the number 14 shows up in 4 out of 5 groups, that's a strong signal. If 37 only shows up in 1 group, it's probably not important.

**Result:**
After this step, you typically have 10-20 "convergent" numbers that passed the test.

---

### Step 6: Score Each Number and Pick the Best

Now we have too many numbers (maybe 15-20) but only need 5 or 6. So we score them!

#### Scoring System (Points):

| What | Points | Meaning |
|------|--------|---------|
| **Direct from pattern** | +10 | Number was directly in a pool (like 14 from 1441) |
| **In your daily verse** | +9 | Your Bible verse for the day contains this number |
| **Digit sum of a number** | +8 | It's the total of a whole message (1441 → 10) |
| **Appears in 80%+ groups** | +7 | Shows up almost everywhere |
| **Common historically** | +5 | This number appears often in past months |
| **Neighbor of a winner** | +5 | It's next to a high-scoring number (if 35 scores high, then 34 and 36 get +5) |
| **Special pattern** | +3 | Palindrome like 11, 22, 33, 44, 55 |
| **Multiple recipes** | +2 | Can be made several different ways |

**Example Scoring:**

Let's say we're scoring the number **14**:
- It appears directly in pool from 1441: +10
- It shows up in 4 out of 5 groups (80%): +7
- It's historically common: +5
- **Total: 22 points**

Now let's score **37**:
- It was made with 1-step math (35 + 2): +0 (not direct)
- Only in 2 out of 5 groups: +0 (not convergent)
- Your daily verse was Matthew 9:37, so 37 is in it: +9
- **Total: 9 points**

**Selection:**
1. Sort all numbers by score (highest first)
2. Pick the top 5 or 6 numbers
3. If there's a tie, pick the one made with simpler math
4. If still tied, pick the smaller number

**Final Chosen Numbers:** [5, 14, 23, 35, 47, 50]

---

### Step 7: Calculate Balance (and Maybe Stars)

#### Balance

Balance shows how your chosen numbers are distributed:

- **Low (1-9):** Small numbers
- **Medium (10-29):** Middle numbers
- **High (30-59):** Big numbers

**Example:**
Chosen numbers: [5, 14, 23, 35, 47, 50]
- Low (1-9): just 5 → **1 low**
- Medium (10-29): 14 and 23 → **2 medium**
- High (30-59): 35, 47, 50 → **3 high**

**Balance: (1, 2, 3)**

There's no "perfect" balance. Different days give different distributions and all are valid.

#### Stars (Optional Mode)

If you're using "5+2 mode" (5 numbers + 2 stars), the system picks 2 extra small numbers called "stars" (1-12 range).

**How Stars Are Made:**
1. Find your most common number from the day (if 1441 appeared 5 times, it's dominant)
2. Take its digits: [1, 4, 4, 1]
3. Add them in different combinations:
   - 1+4 = 5
   - 4+4 = 8
   - 1+4+4 = 9
   - 1+4+4+1 = 10
   - 4-1 = 3
4. Pick the 2 highest that are between 1-12
5. **Stars: [10, 9]**

---

## Real Example: Complete Walkthrough

### Your Input:
```
Numbers seen: 1441, 1707, 2323, 1155
Daily verse: Matthew 9:37
Mode: 6-sign (need 6 final numbers)
```

### The Process:

**Step 1: Clean**
- All numbers are valid ✓

**Step 2: Group**
- Group 1: [1441, 1707]
- Group 2: [2323, 1155]

**Step 3: Extract Pools**

Group 1 Pool:
- From 1441: 1, 4, 10, 14, 41, 44
- From 1707: 0, 1, 7, 15, 17, 50 (portal!)
- Combined: {0, 1, 4, 7, 10, 14, 15, 17, 41, 44, 50}

Group 2 Pool:
- From 2323: 2, 3, 5, 10, 23, 32
- From 1155: 1, 5, 11, 15, 55
- Combined: {1, 2, 3, 5, 10, 11, 15, 23, 32, 55}

**Step 4: Generate Candidates**

Group 1 Examples:
- 14 (direct)
- 50 (portal)
- 15 = 14 + 1 (1-step)
- 7 (direct)
- 8 = 7 + 1 (1-step)
- 41 (direct)
- ... (many more)

Group 2 Examples:
- 23 (direct)
- 11 (direct)
- 5 (direct)
- 24 = 23 + 1 (1-step)
- 8 = 3 + 5 (1-step)
- ... (many more)

**Step 5: Convergence Check**

Need to appear in: 70% of 2 = 2 groups (both!)

Numbers in both groups:
- 1 ✓
- 5 ✓
- 10 ✓
- 15 ✓
- Maybe a few others through different math routes

**Step 6: Scoring**

Let's say after scoring we get:
1. 50 - 27 points (portal + convergent + verse-related)
2. 23 - 25 points (direct + convergent + historical)
3. 14 - 22 points (direct + convergent)
4. 37 - 20 points (verse number + 1-step)
5. 15 - 18 points (direct + convergent)
6. 7 - 15 points (direct + versatile)

**Step 7: Balance**

Final numbers: [7, 14, 15, 23, 37, 50]
- Low (1-9): 7 → 1
- Medium (10-29): 14, 15, 23 → 3
- High (30-59): 37, 50 → 2

**Balance: (1, 3, 2)**

---

## Key Concepts Explained Simply

### What is a "Route"?

A route is just the recipe for how a number was made.

Examples:
- **14** → "Direct from 1441" (0 steps)
- **15** → "14 + 1" (1 step)
- **25** → "(14 + 1) + 10" (2 steps)

Simpler routes are better! Direct numbers score highest.

---

### What is "Convergence"?

Convergence means "agreement across groups."

**Analogy:** Imagine 5 friends each recommend restaurants. If 4 friends all recommend the same Italian place, that's strong convergence. If only 1 friend mentions a Thai place, that's weak convergence.

The system trusts numbers that appear in multiple groups because it means multiple patterns are pointing to the same number.

---

### Why 70%?

70% is the threshold for confidence. It's saying "if at least 70% of the groups agree on this number, it's probably important."

- 3 groups → need 3/3 (100%)
- 4 groups → need 3/4 (75%)
- 5 groups → need 4/5 (80%)
- 6 groups → need 5/6 (83%)

It's a flexible rule that adapts to how many groups you have.

---

### What Makes a Number "Good"?

A good candidate number:
1. **Appears in many groups** (convergence)
2. **Comes directly from a pattern** (not through complicated math)
3. **Matches your daily verse**
4. **Has been common in past months**
5. **Is near other good numbers** (neighborhood effect)

---

## Modes: 6-Sign vs 5+2

### 6-Sign Mode (Standard)

- **Output:** 6 numbers
- **Range:** 1 to 59
- **No stars**

Use this as the default.

### 5+2 Mode (Extended)

- **Output:** 5 numbers + 2 stars
- **Number range:** 1 to 50
- **Star range:** 1 to 12
- **Stars come from your most common number**

Use this if you want the extra "stars" feature.

---

## Common Questions

### Q: Is this random?

**No!** Every step follows fixed rules. If you run the same numbers through the system twice, you'll get the same result.

### Q: Why do I need groups?

Groups let us test if a number is "real" or just a coincidence. If a number appears in many groups independently, that's a strong signal.

### Q: What if I only have 3 numbers?

You'll only get 1 group, which means every number in the pool will be considered "convergent" (since 70% of 1 group = 1 group). The system still works but has less filtering.

### Q: What's the minimum input?

At least 2 numbers, each with at least 2 digits. Ideally 6-12 numbers for best results.

### Q: Can I get the same final number twice?

No. Each chosen number is unique. No duplicates in the final result.

### Q: What if two numbers tie in score?

The system has tiebreaker rules:
1. Prefer simpler math (fewer steps)
2. Prefer historically more common
3. Prefer smaller number

### Q: Do I need to provide a Bible verse?

The algorithm expects one for the "verse codified" bonus (+9 points), but it's optional. Without it, numbers can still score well through other bonuses.

### Q: What is the "portal"?

The portal is a special bonus: if any of your numbers contains a zero (like 1707 or 0404), the number "50" automatically gets added to your pool of choices. It's treated as a premium number.

---

## What You Need to Use This System

### Inputs:
1. **Your numbers** (list of repeated numbers from your day)
   - Minimum: 2 numbers
   - Ideal: 6-12 numbers
   - Format: Any format with digits (1441, 17:07, 23-23, etc.)

2. **Your daily Bible verse** (optional)
   - Format: "Book chapter:verse" (e.g., "Matthew 9:37")
   - Extracted: chapter (9), verse (37), sum (46), difference (28)

3. **Mode choice**
   - "6-sign" (6 numbers, 1-59) **← Default**
   - "5+2" (5 numbers 1-50, plus 2 stars 1-12)

4. **Historical frequency data** (optional)
   - A table showing which numbers were common in past months
   - Format: {number: "ALTA" or "MEDIA" or "BAJA"}

### Outputs:
1. **Chosen numbers** (list of 5 or 6)
2. **Balance** (how many low/medium/high)
3. **Stars** (if using 5+2 mode)
4. **Explanation** (shows how each number was made and why it was chosen)

---

## Summary: The Algorithm in One Paragraph

**The BSR system takes your daily repeated numbers, divides them into small groups, extracts smaller numbers from them using pattern rules, combines those numbers with basic math to create candidates, finds which candidates appear across multiple groups (convergence), scores each candidate based on how it was made and how often it appears, and finally picks the top 5 or 6 numbers with the highest scores. The result is a deterministic set of chosen numbers with a balance showing their distribution.**

---

## Visual Summary

```
YOUR NUMBERS                    PROCESS                         OUTPUT
────────────────               ────────────                    ────────────

1441, 1707,                    1. Clean & Verify               ✓ Valid
2323, 1155,         ──────>    2. Group (2-3 each)       ──>   4 groups
0404, 5050                     3. Find Patterns                 Pools created
                               4. Generate Candidates           ~200 options
Daily Verse:                   5. Check Convergence       ──>   ~15 pass
Matthew 9:37        ──────>    6. Score & Select               Top 6 chosen
                               7. Calculate Balance             (L, M, H)
Mode: 6-sign

                                                                RESULT:
                                                                ────────────
                                                                Numbers:
                                                                5, 14, 23,
                                                                35, 47, 50

                                                                Balance:
                                                                (1, 2, 3)
```

---

## Next Steps

To actually use this system, you need:

1. **Reference data:**
   - Sacred Scribes index (list of valid angel numbers)
   - Monthly frequency tables (historical data)

2. **A calculator/program that implements these rules**
   - See the technical documentation for code
   - Or use a web interface (see implementation plan)

3. **Your daily inputs:**
   - Keep a list of repeated numbers you see
   - Note the time they appeared (optional but helpful)
   - Look up your daily Bible verse

---

**That's it! The BSR algorithm in plain language.**

No mystical language. No esoteric concepts. Just pattern recognition, math, and scoring rules.

If you want to build this system yourself, check out:
- `BSR_ALGORITHM_TECHNICAL.md` - Full technical specification for developers
- `BSR_IMPLEMENTATION_PLAN.md` - Complete project structure with code
