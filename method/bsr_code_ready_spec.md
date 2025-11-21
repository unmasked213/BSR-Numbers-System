# BSR 6.0 Decoding System – Code-Ready Specification

This document refines the high-level BSR 6.0 specification into a deterministic blueprint suitable for automation.  It keeps the original rules and philosophy but resolves ambiguities through explicit assumptions.  Wherever a rule is created rather than derived from the source documents, it is marked as an **implementation assumption** and may be adjusted by the project owner.

## 1. Purpose
The BSR 6.0 system converts daily angel number messages into a set of final numbers (“elegidos”) and optionally stars.  It formalises what was an intuitive practice into a repeatable algorithm built on patterns, convergence, historical verification, and optional scoring.  The system has two modes:

- **6-sign mode** – six chosen numbers, each in 1–59.
- **5 + 2 mode** – five chosen numbers in 1–50 and two stars in 1–12.

## 2. Inputs
1. **Angel messages.**  These are repeated or striking number sequences observed during the day.  Before using a message, check that it appears in the Sacred Scribes index; messages not found (e.g. 3666) are discarded:contentReference[oaicite:0]{index=0}.
2. **Scripture verse.**  A daily Bible verse whose chapter/verse numbers and simple sums or differences (e.g. Matthew 9:37 yields 9, 37, 46 = 9+37, 7 = 9-2) may suggest candidates:contentReference[oaicite:1]{index=1}.
3. **Historical context.**  Monthly frequency tables and past cases indicate how common particular numbers and balance distributions are:contentReference[oaicite:2]{index=2}.

Each input day is treated independently; messages from previous or future days do not affect current processing except through historical frequency tables.

## 3. Output categories
For each day, the algorithm produces:

- **Chosen numbers (signos).**  The main set of five or six integers.
- **Stars (estrellas).**  Two single-digit numbers when using 5 + 2 mode.
- **Balance.**  A triple `(L,M,H)` counting how many chosen numbers fall into each range: low = 1–9, medium = 10–29, high = 30–59:contentReference[oaicite:3]{index=3}.  There is no fixed ideal balance; examples such as 5–0–0, 1–4–0, 0–3–3 and 2–2–2 are all valid:contentReference[oaicite:4]{index=4}.

## 4. Definitions

### 4.1 Constellation
A **constellation** is a group of 2 or 3 angel messages processed together:contentReference[oaicite:5]{index=5}.  Multiple constellations are formed from the day’s messages.  The number of constellations depends on message count:

- 3–6 messages ? 2–3 constellations
- 7–10 messages ? 4–6 constellations
- 11–15 messages ? 6–8 constellations:contentReference[oaicite:6]{index=6}

Quality is more important than quantity; form only as many constellations as needed to confirm convergence:contentReference[oaicite:7]{index=7}.

#### 4.1.1 Constellation formation algorithm (implementation assumption)

1. **Normalize messages:** Strip non-digit characters; preserve leading zeros.  Treat each message as a sequence of digits of length n (typically n = 3 or 4).
2. **Sort messages by time received** (if timestamps available) or otherwise by numeric value ascending.
3. **Determine target group size:** Let `m` be the total number of messages.  Compute:

   - `g = m // 3` (integer division) ? number of 3-message constellations.
   - `r = m % 3` ? remainder messages.

   - If `r = 0`: create `g` groups of 3.
   - If `r = 1`: create `g - 1` groups of 3 and `2` groups of 2.
   - If `r = 2`: create `g` groups of 3 and one group of 2.

4. **Group sequentially:** Take messages in sorted order and assign them to constellations according to the computed pattern.  Example: 10 messages ? 3 groups of 3 and one group of 1+2 merged into a 2-message group.

This algorithm ensures reproducible grouping and respects the 2–3 message guideline.  If additional grouping logic (e.g. by similarity) becomes available, replace this section.

### 4.2 Architecture Phase
Before any calculations, examine each constellation to identify structural patterns (“architecture”):contentReference[oaicite:8]{index=8}.  Recognised patterns enable specific extraction rules.

#### 4.2.1 Pattern catalogue and pool extraction

| Pattern | Condition | Pool additions | Notes |
|---|---|---|---|
| **Palíndromo**:contentReference[oaicite:9]{index=9} | The message string reads the same forwards and backwards. | • All contiguous two-digit blocks = 59 (including their reversed forms).  • The sum of all digits. | Example: 3113 ? blocks {31, 13}, mirror of 31 ? 13 (already present), digit sum 3+1+1+3=8. |
| **ABAB / AABB**:contentReference[oaicite:10]{index=10} | Two or four digits form repeated blocks (e.g. 2323 or 2244). | • The base block (e.g. 23 or 22).  • Its mirror (e.g. 32 or 22).  • Digit sum of the block.  • Total digit sum. | Example: 2323 ? 23, 32, (2+3)=5, total sum=2+3+2+3=10. |
| **Espejo**:contentReference[oaicite:11]{index=11} | A two-digit block AB has its reverse BA in the message. | • Both AB and BA.  • Digit sums of AB. | Example: 1441 has 14?41; extract 14, 41, 44, digit sums. |
| **Delta Fijo**:contentReference[oaicite:12]{index=12} | Digits increase or decrease by a fixed step throughout the message (e.g. 1234 or 8642). | • Same pool as ABAB pattern: extract all two-digit blocks and the total digit sum. | Recognise this pattern to note progression; extraction rules follow ABAB. |
| **Portal [0?]**:contentReference[oaicite:13]{index=13} | The message contains a zero. | • Candidate 50 is added to the pool. | The portal value 50 is used only when at least one zero exists and may only appear once per constellation. |
| **Blocks & digits**:contentReference[oaicite:14]{index=14} | Always present. | • All contiguous two-digit substrings = 59 (drop leading zero).  • Each individual digit as an integer.  • Sum of digits of each block.  • Sum of all digits. | Example: 1707 ? two-digit blocks {17, 70, 07?7}; digits {1,7,0,7}; sum of digits=15; sum of each block=1+7, 7+0, 0+7. |
| **Gemelos**:contentReference[oaicite:15]{index=15} | The message contains a repeated digit pair (e.g. 11, 22, 33). | • The double-digit block (e.g. 22).  • Sum of the pair (2+2).  • Product of the pair (2×2). | Example: 2255 ? 22, 55, sums 4 and 10, products 4 and 25. |
| **Digit booster**:contentReference[oaicite:16]{index=16} | Any digit appears more than once. | • Sum of all occurrences of that digit (e.g. 2+2+2+2 for 2222). | This rule is applied per digit per message. |
| **Regla del 15**:contentReference[oaicite:17]{index=17} | The block 15 appears. | • Block 15 and an extra 1 (digit) may be used separately. | Allows using 15 while keeping an unused 1 in the pool. |

The pool is the union of all numbers produced by these rules.  Duplicate values in the pool are recorded once.

#### 4.2.2 Operation rules

1. **Step limit.**  Each candidate number must be produced from the pool using at most two arithmetic operations (steps).  One “step” may contain multiple additions or multiplications grouped together:contentReference[oaicite:18]{index=18}.  Concatenations are not allowed.  

   - *Definition:* A **step** is a single arithmetic expression combining pool elements with one operator (e.g. `2+3+5` or `2×3×4` counts as one step).  Subtractions and divisions count as separate steps even when chained; oriented subtraction always uses the larger term first:contentReference[oaicite:19]{index=19}.  
   - Example: 23 (pool) minus 1 (from digit 1) = 22 ? 1 step.  Then 22 plus 1 = 23 (undo), second step.  
   - Divisions are only permitted when they yield an integer result:contentReference[oaicite:20]{index=20}.  
   - Roots, powers and decimals are disallowed:contentReference[oaicite:21]{index=21}.

2. **Portal usage.**  If the portal is activated, 50 can be combined with a pool number in one step (e.g. 50 - 44) and may count as the first of two steps.  Portal is never combined with itself or used more than once per route.

3. **Digit re-use.**  “Digit booster” allows the same digit to be used multiple times in one step only.  The digit booster is applied per message and resets when moving to another message.

4. **Result limits.**  In 6-sign mode, any candidate number > 59 is discarded immediately.  In 5 + 2 mode, candidate numbers > 50 are discarded (stars have their own range 1–12).  These limits apply during pool, expansions and final selection.

### 4.3 Routes and prioritisation

After generating the pool for a constellation, compute all possible candidate numbers reachable in one or two steps according to the operation rules.  Each candidate has a **route** (the sequence of operations) and a **step count**.

Prioritise candidates within each constellation as follows:contentReference[oaicite:22]{index=22}:

1. Direct block (original two-digit pool number or valid digit sum).  
2. Portal route (when portal is active).  
3. One-step route (any other one-step combination).  
4. Two-step route.

If multiple routes yield the same candidate number, keep only the shortest-step route.  If still tied, keep the route with fewer distinct pool elements.

### 4.4 Convergence and candidate selection

1. **Count appearances.**  For each candidate number, count the number of constellations in which it appears (regardless of route).  
2. **Compute threshold.**  Let `C` be the number of constellations.  The minimum number of appearances required for convergence is `H = ceil(0.70 × C)`.  
3. **Convergence set.**  A candidate number belongs to the convergence set if it appears in at least `H` constellations.  
   - Candidates derived directly from a single message (e.g. those generated without combining messages) may be promoted into the convergence set even if they do not meet `H`, provided they appear as direct blocks:contentReference[oaicite:23]{index=23}.
4. **Historical verification.**  For each candidate in the convergence set:
   - Consult the monthly frequency table.  If the candidate is labelled “ALTA” or “MUY ALTA” it gains a +5 frequency bonus:contentReference[oaicite:24]{index=24}; otherwise it gains 0.  
   - Check whether the resulting balance (low/medium/high counts) matches the typical balances of the month (e.g. 1–4–0 or 0–3–3).  Candidates that produce very atypical balances are deprioritised.  
   - Check whether the candidate is suggested by the verse (chapter, verse, sums, differences).  Candidates codified in the verse receive +9:contentReference[oaicite:25]{index=25}.

### 4.5 Scoring (optional)

If more than six (or five) candidates remain after convergence and historical verification, apply the scoring system as a tiebreaker.  Each candidate receives points according to:

- +10 – Candidate exists directly as a block in any constellation:contentReference[oaicite:26]{index=26}.
- +9 – Candidate is codified in the verse (chapter/verse or verse arithmetic):contentReference[oaicite:27]{index=27}.
- +8 – Candidate is the angel-root (digit sum) of a message:contentReference[oaicite:28]{index=28}.
- +7 – Candidate achieves high convergence (= 80 %):contentReference[oaicite:29]{index=29}.
- +5 – Candidate appears frequently in cases of the current month:contentReference[oaicite:30]{index=30}.
- +5 – Candidate is a neighbour (family connected) of a high-scoring candidate (see neighbour rule below).  
- +3 – Candidate has a special pattern (palindrome, mirror, master number 11,22,33,44,55):contentReference[oaicite:31]{index=31}.
- +2 – Candidate has multiple independent one-step routes (versatile):contentReference[oaicite:32]{index=32}.

Stars receive points according to a separate table (codified in verse, high convergence, frequent as star, root sum, multiple clean routes, thematic resonance):contentReference[oaicite:33]{index=33}.

### 4.6 Family / Neighbour rule (implementation assumption)

For candidate number `x` that scores +7 or more, its **neighbours** are defined as the numbers `x-1` and `x+1` (provided they remain within the allowed range).  These neighbour candidates receive a +5 bonus.  Example: if 35 scores +7, then 34 and 36 each get +5.  

Only one generation of neighbours is considered; no transitive propagation (i.e. 34’s neighbours do not also gain bonus).  

### 4.7 Final selection algorithm

At the end of processing:

1. **Combine sets:** Start with all convergent candidates.  If more numbers are needed to reach the required count (six for 6-sign mode, five for 5 + 2 mode), add candidates in descending order of total score (including bonuses).  If there are still ties, choose the candidate with the shortest route; if still tied, choose the candidate with the highest historical frequency rank; if still tied, choose the lower numeric value.
2. **Apply range constraints:** Remove any candidate outside the valid range (1–59 for 6-sign mode, 1–50 for 5 + 2 mode).  If removal leaves too few numbers, repeat the score-based filling step with remaining candidates.
3. **Compute balance:** Count how many chosen numbers fall into low (1–9), medium (10–29) and high (30–59) ranges:contentReference[oaicite:34]{index=34}.  Note the balance but do not enforce any distribution; examples such as 5-0-0 and 1-4-0 are valid:contentReference[oaicite:35]{index=35}.
4. **Select stars (if 5 + 2 mode):** Extract the dominant message (see §4.8) and derive stars as described in §4.8; then add them to the output.

### 4.8 Star extraction

Stars originate from a **single dominant angel message**:contentReference[oaicite:36]{index=36}.  They do not require convergence across constellations.  Extract two stars as follows:

1. **Dominant message selection (implementation assumption):**  
   - Count how many times each message appears during the day.  Select the message with the highest count.  
   - If two messages tie, choose the one that appeared earliest in the day.  
   - If still tied, choose the numerically smallest message.  
   - The chosen message is the **dominant message**.

2. **Star generation:** Treat the dominant message as a string of digits.  Compute all one-step sums and subtractions of its digits in groups of two, three or four digits such that the result lies in 1–12.  For example, 1441 ? 1+1=2; 1+4+4+1=10.  Compute all possible distinct results and choose the two highest results as stars.  
   - If fewer than two results exist, pad with zeros or repeat the only available star.  
   - Ignore portal rules when extracting stars; stars are derived directly from the message’s digits:contentReference[oaicite:37]{index=37}.

3. **Star scoring (optional):** Apply the star scoring table if there are more than two candidates (codified in the verse, high convergence, frequent as star, root sum, multiple clean routes, resonance with theme):contentReference[oaicite:38]{index=38}.

### 4.9 Ladders (escaleras)

Ladder sequences (e.g. 0004–0005–0006–0007) do **not** predict the chosen numbers.  Instead, they indicate that high-range numbers (30–50 or 50–59) will be activated:contentReference[oaicite:39]{index=39}.  Implementation rules:

- **Baja ladder (1–10)** ? add a +2 bonus to candidates in the 30–50 range.  
- **Initial ladder (5–8)** ? add a +2 bonus to all candidates; further research needed; treat as neutral if uncertain.  
- **Scaled portal ladder (e.g. 0001–0031–0101–0100)** ? add a +3 bonus to candidates in the 50–59 range.  

No ladder ever forces inclusion of its own numbers.  Ladder bonuses apply after scoring.

### 4.10 Input normalisation (implementation assumption)

- **Whitespace and separators:** Remove spaces, hyphens, dots or other separators between digits.  E.g. “0004” and “0 0 0 4” both become “0004”.  
- **Leading zeros:** Preserve leading zeros for architecture recognition; treat “07” as the block 7 (07?7).  
- **Minimum length:** Messages must contain at least two digits; single-digit messages are ignored.  
- **Duplicate messages:** If the same message appears multiple times, each occurrence is counted separately for constellation formation and dominance, but only one pool is created per constellation.  
- **Mixed length:** Messages of differing lengths may be grouped together.  Extraction rules apply to each message separately.

### 4.11 Mode-specific constraints

| Parameter               | 6-sign mode                    | 5 + 2 mode                  |
|------------------------|--------------------------------|-----------------------------|
| Candidate range        | 1 – 59                         | 1 – 50                     |
| Star extraction        | Not performed                 | Required                   |
| Portal usage           | Always allowed (when 0):contentReference[oaicite:40]{index=40} | Allowed; portal result must lie = 50 |
| Ladder bonuses         | Apply to candidates 30–59      | Apply to candidates 30–50  |

## 5. Seven guiding principles
The philosophical guidelines remain unchanged:contentReference[oaicite:41]{index=41}:
1. **Quality over quantity.**  Use only the necessary constellations to confirm convergence.
2. **Historical verification.**  Consult monthly frequency tables; frequent numbers are strong candidates.
3. **Valid angel messages.**  Check every message against the Sacred Scribes index.:contentReference[oaicite:42]{index=42}
4. **Convergence rules.**  Convergence in 70–80 % of constellations has priority over architectural features.:contentReference[oaicite:43]{index=43}
5. **Flexible balance.**  Accept the day’s balance distribution without forcing a formula:contentReference[oaicite:44]{index=44}.
6. **Verse as guide.**  Use the verse for numeric hints and thematic resonance:contentReference[oaicite:45]{index=45}.
7. **Intuition validates, not decides.**  Data and convergence make the decision; intuition may confirm but not override.

## 6. Usage summary (algorithm outline)

1. **Prepare inputs:** Normalise and verify messages; extract numeric hints from the verse; load the monthly frequency table.
2. **Group messages into constellations** deterministically as per §4.1.1.
3. **For each constellation:** Identify patterns; build the pool (§4.2.1); generate candidate numbers via operations (§4.2.2); prioritise routes (§4.3).
4. **Collect candidates across constellations** and determine convergence (§4.4).  Apply historical verification.
5. **Apply scoring** if more candidates remain than needed.  Include ladder bonuses and neighbour bonuses.  Sort candidates by total points.
6. **Select final numbers** as per §4.7, ensuring range compliance.  Compute and record the balance.
7. **Extract stars** (if 5 + 2 mode) by determining the dominant message and performing direct digit sums (§4.8).
8. **Document the process** for auditing, including pools, routes, scores and reasoning.

This specification provides a deterministic pathway from daily inputs to a stable set of outputs.  It reflects the core rules of BSR 6.0 and clarifies missing details to enable automation.  Assumptions marked explicitly can be refined as more guidance becomes available from the method’s creator.
