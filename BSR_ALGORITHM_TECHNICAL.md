# BSR Algorithm for Developers
## Complete Technical Specification

**Version:** 1.0
**Date:** 2025-11-21
**Base:** BSR 6.0 System

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [System Overview](#system-overview)
3. [Data Structures](#data-structures)
4. [Complete Algorithm Flow](#complete-algorithm-flow)
5. [Phase 1: Input Processing](#phase-1-input-processing)
6. [Phase 2: Constellation Formation](#phase-2-constellation-formation)
7. [Phase 3: Architecture Analysis & Pool Generation](#phase-3-architecture-analysis--pool-generation)
8. [Phase 4: Candidate Generation](#phase-4-candidate-generation)
9. [Phase 5: Convergence Analysis](#phase-5-convergence-analysis)
10. [Phase 6: Scoring & Selection](#phase-6-scoring--selection)
11. [Phase 7: Star Extraction](#phase-7-star-extraction)
12. [Implementation Examples](#implementation-examples)
13. [Edge Cases & Validation](#edge-cases--validation)

---

## Executive Summary

The BSR (Butterfly Spiritual Resonance) 6.0 system is a **deterministic algorithm** that transforms a daily set of repeated number sequences ("angel messages") into a final set of chosen numbers (elegidos) and optional stars.

**Input:** List of number sequences (e.g., `["1441", "1707", "2323", "1155"]`)
**Output:**
- 6 numbers (range 1-59) **OR** 5 numbers (range 1-50) + 2 stars (range 1-12)
- Balance tuple: `(low_count, medium_count, high_count)` where low=1-9, medium=10-29, high=30-59

**Core Principle:** Pattern recognition → Candidate generation → Convergence filtering → Historical verification → Scoring → Final selection

---

## System Overview

### Two Operating Modes

| Mode | Output | Number Range | Stars | Use Case |
|------|--------|--------------|-------|----------|
| **6-sign** | 6 numbers | 1-59 | None | Default mode |
| **5+2** | 5 numbers + 2 stars | Numbers: 1-50<br>Stars: 1-12 | Required | Extended mode |

### Key Concepts

1. **Angel Messages**: Input sequences (e.g., 1441, 1707, 2323)
2. **Constellations**: Groups of 2-3 messages processed together
3. **Pool**: Set of candidate numbers extracted from each constellation
4. **Routes**: Arithmetic operations transforming pool numbers into candidates
5. **Convergence**: Candidates appearing across multiple constellations
6. **Elegidos**: Final chosen numbers

---

## Data Structures

```python
class Message:
    """A single angel message"""
    value: str           # Raw string (e.g., "1441")
    timestamp: datetime  # When received (optional)
    digits: List[int]    # [1, 4, 4, 1]

class Constellation:
    """Group of 2-3 messages"""
    messages: List[Message]
    pool: Set[int]       # Extracted numbers
    patterns: List[str]  # Identified patterns
    candidates: Dict[int, List[Route]]  # candidate -> routes

class Route:
    """Arithmetic path to generate a candidate"""
    result: int
    steps: int           # 0 (direct), 1, or 2
    operations: str      # Human-readable formula
    pool_elements: List[int]
    route_type: str      # 'direct', 'portal', 'one-step', 'two-step'

class Candidate:
    """A candidate number being evaluated"""
    value: int
    appearances: int     # Count across constellations
    best_route: Route
    score: int
    bonuses: Dict[str, int]  # Bonus type -> points

class Result:
    """Final output"""
    elegidos: List[int]
    stars: List[int]     # Only in 5+2 mode
    balance: Tuple[int, int, int]  # (low, medium, high)
    metadata: Dict       # Processing details
```

---

## Complete Algorithm Flow

```
┌─────────────────────────────────────────┐
│ INPUT: Angel Messages                   │
│ ["1441", "1707", "2323", "1155", ...]  │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ PHASE 1: Input Processing               │
│ • Normalize messages                    │
│ • Verify against Sacred Scribes index   │
│ • Extract verse numbers                 │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ PHASE 2: Constellation Formation        │
│ • Group into 2-3 message clusters       │
│ • Sort by timestamp or numeric value    │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ PHASE 3: Architecture Analysis          │
│ FOR EACH CONSTELLATION:                 │
│ • Identify patterns (portal, mirror...) │
│ • Extract pool numbers                  │
│ • Apply pattern rules                   │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ PHASE 4: Candidate Generation           │
│ FOR EACH CONSTELLATION:                 │
│ • Generate 0-step (direct pool)         │
│ • Generate 1-step operations            │
│ • Generate 2-step operations            │
│ • Filter by range (1-59 or 1-50)       │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ PHASE 5: Convergence Analysis           │
│ • Count appearances across clusters     │
│ • Calculate threshold (70% × clusters)  │
│ • Filter convergent candidates          │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ PHASE 6: Scoring & Selection            │
│ • Apply scoring rules (+10, +9, +8...)  │
│ • Add historical frequency bonuses      │
│ • Add verse alignment bonuses           │
│ • Add neighbour bonuses                 │
│ • Select top 5 or 6 candidates          │
│ • Calculate balance (L/M/H)             │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ PHASE 7: Star Extraction (5+2 mode)     │
│ • Identify dominant message             │
│ • Extract digit combinations → 1-12     │
│ • Select top 2 as stars                 │
└────────────────┬────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────┐
│ OUTPUT: Elegidos + Stars + Balance      │
│ [5, 14, 23, 35, 47, 50]                │
│ Stars: [2, 10]                          │
│ Balance: (1, 3, 2)                      │
└─────────────────────────────────────────┘
```

---

## Phase 1: Input Processing

### 1.1 Message Normalization

```python
def normalize_message(raw: str) -> str:
    """
    Normalize a raw angel message.

    Rules:
    - Remove spaces, hyphens, dots, separators
    - Preserve leading zeros
    - Must contain at least 2 digits
    - Only keep digit characters

    Examples:
    - "0 0 0 4" → "0004"
    - "14-41" → "1441"
    - "1.7.0.7" → "1707"
    """
    # Remove all non-digit characters
    cleaned = ''.join(c for c in raw if c.isdigit())

    # Validate minimum length
    if len(cleaned) < 2:
        raise ValueError(f"Message too short: {raw}")

    return cleaned
```

### 1.2 Sacred Scribes Verification

```python
def verify_sacred_scribes(message: str, index: Set[str]) -> bool:
    """
    Verify message appears in Sacred Scribes angel number index.

    Note: Index must be loaded from external source.
    Messages not in index are discarded (e.g., 3666).
    """
    return message in index
```

### 1.3 Verse Extraction

```python
def extract_verse_numbers(verse: str) -> List[int]:
    """
    Extract candidate numbers from Bible verse reference.

    Example: "Matthew 9:37"
    Returns: [9, 37, 46, 7]
    Where:
    - 9: chapter
    - 37: verse
    - 46: 9 + 37
    - 7: 37 - 9 (always larger - smaller)
    """
    # Parse verse format: "Book chapter:verse"
    # Implementation depends on input format
    pass
```

---

## Phase 2: Constellation Formation

### 2.1 Grouping Algorithm

```python
def form_constellations(messages: List[Message]) -> List[Constellation]:
    """
    Group messages into constellations of 2-3 messages each.

    Algorithm:
    1. Sort messages by timestamp (if available) or numeric value
    2. Calculate: g = len(messages) // 3, r = len(messages) % 3
    3. If r == 0: Create g groups of 3
    4. If r == 1: Create (g-1) groups of 3 and 2 groups of 2
    5. If r == 2: Create g groups of 3 and 1 group of 2

    Example: 10 messages
    - g = 10 // 3 = 3
    - r = 10 % 3 = 1
    - Result: 2 groups of 3, 2 groups of 2
    """
    m = len(messages)
    g = m // 3
    r = m % 3

    constellations = []
    idx = 0

    if r == 0:
        # g groups of 3
        for _ in range(g):
            constellations.append(Constellation(messages[idx:idx+3]))
            idx += 3
    elif r == 1:
        # (g-1) groups of 3, then 2 groups of 2
        for _ in range(g - 1):
            constellations.append(Constellation(messages[idx:idx+3]))
            idx += 3
        constellations.append(Constellation(messages[idx:idx+2]))
        idx += 2
        constellations.append(Constellation(messages[idx:idx+2]))
    else:  # r == 2
        # g groups of 3, then 1 group of 2
        for _ in range(g):
            constellations.append(Constellation(messages[idx:idx+3]))
            idx += 3
        constellations.append(Constellation(messages[idx:idx+2]))

    return constellations
```

### 2.2 Expected Constellation Count

| Total Messages | Expected Constellations |
|----------------|------------------------|
| 3-6 | 2-3 |
| 7-10 | 4-6 |
| 11-15 | 6-8 |

---

## Phase 3: Architecture Analysis & Pool Generation

### 3.1 Pattern Recognition

For each constellation, identify these patterns:

```python
def analyze_patterns(constellation: Constellation) -> List[str]:
    """
    Identify structural patterns in constellation messages.

    Returns list of pattern names found.
    """
    patterns = []

    for msg in constellation.messages:
        # Check each pattern type
        if is_palindrome(msg):
            patterns.append('palindrome')
        if has_abab(msg):
            patterns.append('abab')
        if has_mirror(msg):
            patterns.append('mirror')
        if has_delta(msg):
            patterns.append('delta')
        if has_portal(msg):
            patterns.append('portal')
        if has_twins(msg):
            patterns.append('twins')
        # ... etc

    return patterns
```

### 3.2 Pattern Definitions & Pool Extraction

#### **Pattern: Palindrome**

```python
def is_palindrome(msg: Message) -> bool:
    return msg.value == msg.value[::-1]

def extract_palindrome(msg: Message) -> Set[int]:
    """
    Example: "3113"
    Extracts:
    - Two-digit blocks: 31, 13
    - Digit sum: 3+1+1+3 = 8
    Returns: {31, 13, 8}
    """
    pool = set()

    # Extract all 2-digit blocks
    for i in range(len(msg.value) - 1):
        block = msg.value[i:i+2]
        pool.add(int(block))
        # Mirror is automatically included for palindromes

    # Digit sum
    digit_sum = sum(msg.digits)
    if digit_sum <= 59:  # Or 50 in 5+2 mode
        pool.add(digit_sum)

    return pool
```

#### **Pattern: ABAB / AABB**

```python
def has_abab(msg: Message) -> bool:
    """Check for repeated 2-digit blocks"""
    if len(msg.value) == 4:
        return msg.value[0:2] == msg.value[2:4]  # AABB
    # For ABAB: 2323 → "23" repeated
    # Implementation varies by message length
    return False

def extract_abab(msg: Message) -> Set[int]:
    """
    Example: "2323"
    Extracts:
    - Base block: 23
    - Mirror: 32
    - Block digit sum: 2+3 = 5
    - Total digit sum: 2+3+2+3 = 10
    Returns: {23, 32, 5, 10}
    """
    pool = set()

    if len(msg.value) == 4:
        block = msg.value[0:2]
        pool.add(int(block))
        pool.add(int(block[::-1]))  # Mirror
        pool.add(sum(int(d) for d in block))  # Block sum
        pool.add(sum(msg.digits))  # Total sum

    return pool
```

#### **Pattern: Mirror (Espejo)**

```python
def has_mirror(msg: Message) -> bool:
    """Check if 2-digit block has its reverse in the message"""
    value = msg.value
    for i in range(len(value) - 1):
        block = value[i:i+2]
        reverse = block[::-1]
        if reverse in value and block != reverse:
            return True
    return False

def extract_mirror(msg: Message) -> Set[int]:
    """
    Example: "1441" has 14↔41
    Extracts:
    - 14, 41
    - All digit pairs present (44)
    - Digit sums
    Returns: {14, 41, 44, 5, 8}
    """
    pool = set()

    # Find all mirror pairs
    value = msg.value
    for i in range(len(value) - 1):
        block = value[i:i+2]
        pool.add(int(block))
        reverse = block[::-1]
        if reverse in value:
            pool.add(int(reverse))

    # Digit sums
    pool.add(sum(msg.digits))

    return pool
```

#### **Pattern: Portal (0 present)**

```python
def has_portal(msg: Message) -> bool:
    return '0' in msg.value

def extract_portal(msg: Message) -> Set[int]:
    """
    If message contains 0, add 50 to pool.
    Portal can only be used once per constellation.

    Example: "1707" contains 0
    Returns: {50}
    """
    if '0' in msg.value:
        return {50}
    return set()
```

#### **Pattern: Twins (Gemelos)**

```python
def has_twins(msg: Message) -> bool:
    """Check for repeated digit pairs: 11, 22, 33, etc."""
    for i in range(len(msg.value) - 1):
        if msg.value[i] == msg.value[i+1]:
            return True
    return False

def extract_twins(msg: Message) -> Set[int]:
    """
    Example: "2255"
    Extracts:
    - Twin blocks: 22, 55
    - Sums: 2+2=4, 5+5=10
    - Products: 2×2=4, 5×5=25
    Returns: {22, 55, 4, 10, 25}
    """
    pool = set()

    for i in range(len(msg.value) - 1):
        if msg.value[i] == msg.value[i+1]:
            digit = int(msg.value[i])
            twin_value = digit * 11  # 2→22, 5→55
            pool.add(twin_value)
            pool.add(digit + digit)  # Sum
            pool.add(digit * digit)  # Product

    return pool
```

#### **Pattern: Delta Fijo (Fixed Step)**

```python
def has_delta(msg: Message) -> bool:
    """Check if digits form arithmetic sequence"""
    diffs = [msg.digits[i+1] - msg.digits[i] for i in range(len(msg.digits)-1)]
    return len(set(diffs)) == 1  # All differences are equal

def extract_delta(msg: Message) -> Set[int]:
    """
    Example: "1234" (step +1) or "8642" (step -2)
    Extraction follows ABAB pattern rules.
    """
    return extract_abab(msg)  # Same extraction rules
```

#### **Pattern: Digit Booster**

```python
def extract_digit_booster(msg: Message) -> Set[int]:
    """
    If digit D appears N times, add D×N to pool.

    Example: "2222"
    - Digit 2 appears 4 times
    - Add 2+2+2+2 = 8
    Returns: {8}
    """
    pool = set()
    digit_counts = {}

    for digit in msg.digits:
        digit_counts[digit] = digit_counts.get(digit, 0) + 1

    for digit, count in digit_counts.items():
        if count > 1:
            pool.add(digit * count)

    return pool
```

#### **Pattern: Rule of 15**

```python
def extract_rule_15(msg: Message) -> Set[int]:
    """
    If block "15" appears, extract both 15 and extra 1.

    Example: "1505"
    - Contains "15"
    - Extract 15 (as block) and 1 (as separate digit)
    """
    if '15' in msg.value:
        return {15, 1}
    return set()
```

#### **Universal Extraction (Always Applied)**

```python
def extract_blocks_and_digits(msg: Message) -> Set[int]:
    """
    Always extract:
    - All 2-digit contiguous blocks (≤59 or ≤50)
    - All individual digits
    - Sum of each block's digits
    - Total digit sum

    Example: "1707"
    Blocks: 17, 70→skip(>59), 07→7
    Digits: 1, 7, 0, 7
    Block sums: 1+7=8, 7+0=7, 0+7=7
    Total sum: 1+7+0+7=15
    Returns: {17, 7, 1, 0, 8, 15}
    """
    pool = set()

    # Extract 2-digit blocks
    for i in range(len(msg.value) - 1):
        block_str = msg.value[i:i+2]
        block_val = int(block_str)

        # Apply range filter (59 for 6-sign, 50 for 5+2)
        if block_val <= 59:  # Adjust for mode
            pool.add(block_val)

        # Block digit sum
        block_sum = int(block_str[0]) + int(block_str[1])
        pool.add(block_sum)

    # Extract individual digits
    for digit in msg.digits:
        pool.add(digit)

    # Total digit sum
    total_sum = sum(msg.digits)
    if total_sum <= 59:  # Adjust for mode
        pool.add(total_sum)

    return pool
```

### 3.3 Complete Pool Building

```python
def build_constellation_pool(constellation: Constellation, mode: str) -> Set[int]:
    """
    Build complete pool for a constellation by applying all patterns.

    Args:
        constellation: Group of 2-3 messages
        mode: '6-sign' or '5+2'

    Returns:
        Set of all candidate numbers extracted
    """
    pool = set()
    max_value = 59 if mode == '6-sign' else 50

    for msg in constellation.messages:
        # Always extract blocks and digits
        pool.update(extract_blocks_and_digits(msg))

        # Pattern-specific extractions
        if is_palindrome(msg):
            pool.update(extract_palindrome(msg))
        if has_abab(msg):
            pool.update(extract_abab(msg))
        if has_mirror(msg):
            pool.update(extract_mirror(msg))
        if has_delta(msg):
            pool.update(extract_delta(msg))
        if has_portal(msg):
            pool.update(extract_portal(msg))
        if has_twins(msg):
            pool.update(extract_twins(msg))

        pool.update(extract_digit_booster(msg))
        pool.update(extract_rule_15(msg))

    # Filter by range
    pool = {n for n in pool if 1 <= n <= max_value}

    return pool
```

---

## Phase 4: Candidate Generation

### 4.1 Operation Rules

```python
class OperationRules:
    """
    Rules for generating candidates from pool.

    - Maximum 2 steps
    - One step can contain multiple same-operator operations
    - Subtraction: always larger - smaller
    - Division: only if result is integer
    - No concatenation, powers, roots, decimals
    """

    @staticmethod
    def is_valid_step(operations: str) -> bool:
        """Validate operation string"""
        # Implementation: check for valid operators, proper formatting
        pass
```

### 4.2 Route Types & Prioritization

```python
class RouteType(Enum):
    DIRECT = 0      # Number directly in pool (0 steps)
    PORTAL = 1      # Uses portal (50) in operation
    ONE_STEP = 2    # Single arithmetic operation
    TWO_STEP = 3    # Two sequential operations

# Priority order: DIRECT > PORTAL > ONE_STEP > TWO_STEP
```

### 4.3 Candidate Generation Functions

```python
def generate_direct_candidates(pool: Set[int]) -> Dict[int, Route]:
    """
    0-step routes: numbers already in pool.

    Returns: {number: Route(steps=0, type='direct')}
    """
    return {
        n: Route(
            result=n,
            steps=0,
            operations=str(n),
            pool_elements=[n],
            route_type='direct'
        )
        for n in pool
    }

def generate_one_step_candidates(pool: Set[int], portal: bool, max_val: int) -> Dict[int, List[Route]]:
    """
    1-step routes: single arithmetic operation.

    Operations:
    - Addition: a + b + c + ...
    - Multiplication: a × b × c × ...
    - Subtraction: max(a,b) - min(a,b)
    - Division: a / b (if integer result)
    - Portal: 50 ± pool_element (if portal active)

    Returns: {candidate: [Route1, Route2, ...]}
    """
    candidates = {}
    pool_list = list(pool)

    # Addition combinations
    for i in range(len(pool_list)):
        for j in range(i, len(pool_list)):
            result = pool_list[i] + pool_list[j]
            if 1 <= result <= max_val:
                route = Route(
                    result=result,
                    steps=1,
                    operations=f"{pool_list[i]} + {pool_list[j]}",
                    pool_elements=[pool_list[i], pool_list[j]],
                    route_type='one-step'
                )
                candidates.setdefault(result, []).append(route)

            # Triple additions
            for k in range(j, len(pool_list)):
                result = pool_list[i] + pool_list[j] + pool_list[k]
                if 1 <= result <= max_val:
                    route = Route(
                        result=result,
                        steps=1,
                        operations=f"{pool_list[i]} + {pool_list[j]} + {pool_list[k]}",
                        pool_elements=[pool_list[i], pool_list[j], pool_list[k]],
                        route_type='one-step'
                    )
                    candidates.setdefault(result, []).append(route)

    # Multiplication combinations
    for i in range(len(pool_list)):
        for j in range(i, len(pool_list)):
            result = pool_list[i] * pool_list[j]
            if 1 <= result <= max_val:
                route = Route(
                    result=result,
                    steps=1,
                    operations=f"{pool_list[i]} × {pool_list[j]}",
                    pool_elements=[pool_list[i], pool_list[j]],
                    route_type='one-step'
                )
                candidates.setdefault(result, []).append(route)

    # Subtraction combinations (always larger - smaller)
    for i in range(len(pool_list)):
        for j in range(i + 1, len(pool_list)):
            a, b = pool_list[i], pool_list[j]
            result = abs(a - b)
            if 1 <= result <= max_val:
                route = Route(
                    result=result,
                    steps=1,
                    operations=f"{max(a,b)} - {min(a,b)}",
                    pool_elements=[a, b],
                    route_type='one-step'
                )
                candidates.setdefault(result, []).append(route)

    # Division combinations (integer results only)
    for i in range(len(pool_list)):
        for j in range(len(pool_list)):
            if i != j and pool_list[j] != 0:
                if pool_list[i] % pool_list[j] == 0:
                    result = pool_list[i] // pool_list[j]
                    if 1 <= result <= max_val:
                        route = Route(
                            result=result,
                            steps=1,
                            operations=f"{pool_list[i]} / {pool_list[j]}",
                            pool_elements=[pool_list[i], pool_list[j]],
                            route_type='one-step'
                        )
                        candidates.setdefault(result, []).append(route)

    # Portal operations (if portal active)
    if portal and 50 not in pool:
        for p in pool_list:
            # 50 + p
            result = 50 + p
            if 1 <= result <= max_val:
                route = Route(
                    result=result,
                    steps=1,
                    operations=f"50 + {p}",
                    pool_elements=[50, p],
                    route_type='portal'
                )
                candidates.setdefault(result, []).append(route)

            # 50 - p or p - 50 (whichever is positive)
            if 50 > p:
                result = 50 - p
                if 1 <= result <= max_val:
                    route = Route(
                        result=result,
                        steps=1,
                        operations=f"50 - {p}",
                        pool_elements=[50, p],
                        route_type='portal'
                    )
                    candidates.setdefault(result, []).append(route)

    return candidates

def generate_two_step_candidates(pool: Set[int], one_step_results: Set[int], max_val: int) -> Dict[int, List[Route]]:
    """
    2-step routes: apply operations to one-step results.

    Strategy:
    - Take results from 1-step operations
    - Apply second operation with pool elements
    - Track full operation chain

    Returns: {candidate: [Route1, Route2, ...]}
    """
    candidates = {}

    # Combine one-step results with pool elements
    for intermediate in one_step_results:
        for pool_elem in pool:
            # Addition
            result = intermediate + pool_elem
            if 1 <= result <= max_val:
                route = Route(
                    result=result,
                    steps=2,
                    operations=f"({intermediate}) + {pool_elem}",
                    pool_elements=[intermediate, pool_elem],
                    route_type='two-step'
                )
                candidates.setdefault(result, []).append(route)

            # Subtraction
            result = abs(intermediate - pool_elem)
            if 1 <= result <= max_val:
                route = Route(
                    result=result,
                    steps=2,
                    operations=f"{max(intermediate, pool_elem)} - {min(intermediate, pool_elem)}",
                    pool_elements=[intermediate, pool_elem],
                    route_type='two-step'
                )
                candidates.setdefault(result, []).append(route)

            # Multiplication
            result = intermediate * pool_elem
            if 1 <= result <= max_val:
                route = Route(
                    result=result,
                    steps=2,
                    operations=f"({intermediate}) × {pool_elem}",
                    pool_elements=[intermediate, pool_elem],
                    route_type='two-step'
                )
                candidates.setdefault(result, []).append(route)

            # Division
            if pool_elem != 0 and intermediate % pool_elem == 0:
                result = intermediate // pool_elem
                if 1 <= result <= max_val:
                    route = Route(
                        result=result,
                        steps=2,
                        operations=f"{intermediate} / {pool_elem}",
                        pool_elements=[intermediate, pool_elem],
                        route_type='two-step'
                    )
                    candidates.setdefault(result, []).append(route)

    return candidates
```

### 4.4 Best Route Selection

```python
def select_best_route(routes: List[Route]) -> Route:
    """
    When multiple routes produce same candidate, select best:

    Priority:
    1. Fewer steps (direct > portal > one-step > two-step)
    2. Route type (direct > portal > one-step > two-step)
    3. Fewer pool elements used
    4. Simplest operations
    """
    if not routes:
        return None

    # Sort by priority
    sorted_routes = sorted(routes, key=lambda r: (
        r.steps,
        0 if r.route_type == 'direct' else 1 if r.route_type == 'portal' else 2 if r.route_type == 'one-step' else 3,
        len(r.pool_elements)
    ))

    return sorted_routes[0]
```

---

## Phase 5: Convergence Analysis

### 5.1 Convergence Threshold

```python
def calculate_convergence_threshold(num_constellations: int) -> int:
    """
    Threshold = ceil(0.70 × number_of_constellations)

    Examples:
    - 3 constellations → ceil(2.1) = 3 (100%)
    - 4 constellations → ceil(2.8) = 3 (75%)
    - 5 constellations → ceil(3.5) = 4 (80%)
    - 6 constellations → ceil(4.2) = 5 (83%)
    """
    import math
    return math.ceil(0.70 * num_constellations)
```

### 5.2 Convergence Calculation

```python
def analyze_convergence(constellations: List[Constellation]) -> Dict[int, Candidate]:
    """
    Count appearances of each candidate across constellations.
    Filter by convergence threshold.

    Returns: {candidate_value: Candidate object}
    """
    # Count appearances
    candidate_appearances = {}
    candidate_routes = {}

    for constellation in constellations:
        for candidate_value, routes in constellation.candidates.items():
            candidate_appearances[candidate_value] = candidate_appearances.get(candidate_value, 0) + 1
            if candidate_value not in candidate_routes:
                candidate_routes[candidate_value] = []
            candidate_routes[candidate_value].extend(routes)

    # Calculate threshold
    threshold = calculate_convergence_threshold(len(constellations))

    # Filter convergent candidates
    convergent = {}
    for candidate_value, appearances in candidate_appearances.items():
        if appearances >= threshold:
            convergent[candidate_value] = Candidate(
                value=candidate_value,
                appearances=appearances,
                best_route=select_best_route(candidate_routes[candidate_value]),
                score=0,
                bonuses={}
            )

    # Special case: direct blocks with high appearances (even if below threshold)
    for candidate_value, routes in candidate_routes.items():
        if any(r.route_type == 'direct' for r in routes):
            if candidate_value not in convergent:
                convergent[candidate_value] = Candidate(
                    value=candidate_value,
                    appearances=candidate_appearances[candidate_value],
                    best_route=select_best_route(candidate_routes[candidate_value]),
                    score=0,
                    bonuses={}
                )

    return convergent
```

---

## Phase 6: Scoring & Selection

### 6.1 Scoring System

```python
class ScoringRules:
    """Point assignments for candidate evaluation"""

    DIRECT_BLOCK = 10        # Exists as block in constellation
    VERSE_CODIFIED = 9       # Present in verse numbers
    ANGEL_ROOT = 8           # Digit sum of a message
    HIGH_CONVERGENCE = 7     # Appears in ≥80% constellations
    FREQUENT = 5             # High frequency in monthly table
    NEIGHBOUR = 5            # Adjacent to high-scoring candidate
    SPECIAL_PATTERN = 3      # Palindrome, mirror, master number
    VERSATILE = 2            # Multiple independent routes

def apply_scoring(candidate: Candidate,
                  constellations: List[Constellation],
                  verse_numbers: List[int],
                  frequency_table: Dict[int, str]) -> int:
    """
    Calculate total score for a candidate.

    Returns: total score (sum of all bonuses)
    """
    score = 0
    bonuses = {}

    # +10: Direct block
    if candidate.best_route.route_type == 'direct':
        score += ScoringRules.DIRECT_BLOCK
        bonuses['direct_block'] = 10

    # +9: Verse codified
    if candidate.value in verse_numbers:
        score += ScoringRules.VERSE_CODIFIED
        bonuses['verse'] = 9

    # +8: Angel root (digit sum of message)
    for constellation in constellations:
        for msg in constellation.messages:
            if sum(msg.digits) == candidate.value:
                score += ScoringRules.ANGEL_ROOT
                bonuses['angel_root'] = 8
                break

    # +7: High convergence (≥80%)
    convergence_rate = candidate.appearances / len(constellations)
    if convergence_rate >= 0.80:
        score += ScoringRules.HIGH_CONVERGENCE
        bonuses['high_convergence'] = 7

    # +5: Frequent in monthly table
    if frequency_table.get(candidate.value) in ['ALTA', 'MUY ALTA']:
        score += ScoringRules.FREQUENT
        bonuses['frequent'] = 5

    # +3: Special pattern
    if is_special_pattern(candidate.value):
        score += ScoringRules.SPECIAL_PATTERN
        bonuses['special_pattern'] = 3

    # +2: Versatile (multiple routes)
    # Count distinct one-step routes
    # Implementation depends on route tracking

    candidate.score = score
    candidate.bonuses = bonuses
    return score

def is_special_pattern(value: int) -> bool:
    """
    Check if number is special pattern:
    - Palindrome: 11, 22, 33, 44, 55
    - Mirror: 12↔21, 13↔31, etc.
    - Master numbers: 11, 22, 33, 44, 55
    """
    s = str(value)
    if len(s) == 2:
        # Palindrome / master number
        if s[0] == s[1]:
            return True
        # Mirror pairs (defined externally)
        # Implementation specific
    return False
```

### 6.2 Neighbour Bonus

```python
def apply_neighbour_bonus(candidates: Dict[int, Candidate]) -> None:
    """
    For candidates with score ≥7, give +5 to neighbours (±1).

    Modifies candidates in-place.
    Only one generation (no transitive propagation).
    """
    high_scorers = [c for c in candidates.values() if c.score >= 7]

    for high_scorer in high_scorers:
        # Check neighbour -1
        neighbour_down = high_scorer.value - 1
        if neighbour_down in candidates:
            if 'neighbour' not in candidates[neighbour_down].bonuses:
                candidates[neighbour_down].score += ScoringRules.NEIGHBOUR
                candidates[neighbour_down].bonuses['neighbour'] = 5

        # Check neighbour +1
        neighbour_up = high_scorer.value + 1
        if neighbour_up in candidates:
            if 'neighbour' not in candidates[neighbour_up].bonuses:
                candidates[neighbour_up].score += ScoringRules.NEIGHBOUR
                candidates[neighbour_up].bonuses['neighbour'] = 5
```

### 6.3 Ladder Bonuses

```python
def detect_ladder(messages: List[Message]) -> Optional[str]:
    """
    Detect ladder sequences in messages.

    Types:
    - Baja ladder: 0001-0002-0003...0010
    - Initial ladder: 0005-0006-0007-0008
    - Scaled portal: 0001-0031-0101-0100

    Returns: 'baja', 'initial', 'scaled_portal', or None
    """
    # Implementation: check for consecutive sequences
    # Look for patterns in message ordering
    pass

def apply_ladder_bonus(candidates: Dict[int, Candidate], ladder_type: str) -> None:
    """
    Apply ladder bonuses based on detected ladder type.

    - Baja ladder: +2 to candidates 30-50
    - Initial ladder: +2 to all candidates
    - Scaled portal: +3 to candidates 50-59

    Modifies candidates in-place.
    """
    for candidate in candidates.values():
        if ladder_type == 'baja' and 30 <= candidate.value <= 50:
            candidate.score += 2
            candidate.bonuses['ladder_baja'] = 2
        elif ladder_type == 'initial':
            candidate.score += 2
            candidate.bonuses['ladder_initial'] = 2
        elif ladder_type == 'scaled_portal' and 50 <= candidate.value <= 59:
            candidate.score += 3
            candidate.bonuses['ladder_scaled'] = 3
```

### 6.4 Final Selection

```python
def select_final_elegidos(candidates: Dict[int, Candidate],
                          target_count: int,
                          mode: str) -> List[int]:
    """
    Select final chosen numbers.

    Process:
    1. Sort candidates by score (descending)
    2. Break ties by:
       a. Shortest route (fewer steps)
       b. Higher historical frequency
       c. Lower numeric value
    3. Take top N candidates
    4. Ensure range compliance (1-59 or 1-50)

    Args:
        candidates: Dict of candidate objects
        target_count: 6 for 6-sign mode, 5 for 5+2 mode
        mode: '6-sign' or '5+2'

    Returns: List of chosen numbers (sorted ascending)
    """
    max_value = 59 if mode == '6-sign' else 50

    # Filter by range
    valid_candidates = {k: v for k, v in candidates.items() if 1 <= k <= max_value}

    # Sort by priority
    sorted_candidates = sorted(
        valid_candidates.values(),
        key=lambda c: (
            -c.score,              # Higher score first
            c.best_route.steps,    # Fewer steps first
            # Historical frequency would go here
            c.value                # Lower value as final tiebreaker
        )
    )

    # Select top N
    selected = [c.value for c in sorted_candidates[:target_count]]

    # If not enough, this is an error condition
    if len(selected) < target_count:
        raise ValueError(f"Insufficient candidates: {len(selected)} < {target_count}")

    return sorted(selected)
```

### 6.5 Balance Calculation

```python
def calculate_balance(elegidos: List[int]) -> Tuple[int, int, int]:
    """
    Calculate balance distribution: (low, medium, high)

    Ranges:
    - Low: 1-9
    - Medium: 10-29
    - High: 30-59

    Returns: (count_low, count_medium, count_high)
    """
    low = sum(1 for n in elegidos if 1 <= n <= 9)
    medium = sum(1 for n in elegidos if 10 <= n <= 29)
    high = sum(1 for n in elegidos if 30 <= n <= 59)

    return (low, medium, high)
```

---

## Phase 7: Star Extraction

**(Only for 5+2 mode)**

### 7.1 Dominant Message Selection

```python
def select_dominant_message(messages: List[Message]) -> Message:
    """
    Select the dominant message for star extraction.

    Priority:
    1. Highest count (most frequent during day)
    2. Earliest timestamp
    3. Numerically smallest value

    Returns: The dominant message
    """
    # Count occurrences
    message_counts = {}
    for msg in messages:
        message_counts[msg.value] = message_counts.get(msg.value, 0) + 1

    # Find max count
    max_count = max(message_counts.values())

    # Filter messages with max count
    candidates = [msg for msg in messages if message_counts[msg.value] == max_count]

    # Sort by timestamp (earliest first), then numeric value
    candidates.sort(key=lambda m: (m.timestamp if m.timestamp else float('inf'), int(m.value)))

    return candidates[0]
```

### 7.2 Star Generation

```python
def extract_stars(dominant_message: Message) -> List[int]:
    """
    Extract two stars from dominant message.

    Process:
    1. Generate all possible digit combinations (groups of 2, 3, or 4 digits)
    2. Compute sums and subtractions
    3. Filter results to range 1-12
    4. Select top 2 highest values

    Example: "1441"
    - Pairs: 1+4=5, 4+4=8, 4+1=5, 1-4→invalid, 4-4=0→invalid, 4-1=3
    - Triples: 1+4+4=9, 4+4+1=9
    - All: 1+4+4+1=10
    - Valid in range 1-12: [3, 5, 5, 8, 9, 9, 10]
    - Top 2 distinct: [10, 9]

    Returns: [star1, star2] (descending order)
    """
    digits = dominant_message.digits
    star_candidates = set()

    # Pairs
    for i in range(len(digits)):
        for j in range(i + 1, len(digits)):
            # Sum
            result = digits[i] + digits[j]
            if 1 <= result <= 12:
                star_candidates.add(result)

            # Difference
            result = abs(digits[i] - digits[j])
            if 1 <= result <= 12:
                star_candidates.add(result)

    # Triples
    for i in range(len(digits)):
        for j in range(i + 1, len(digits)):
            for k in range(j + 1, len(digits)):
                result = digits[i] + digits[j] + digits[k]
                if 1 <= result <= 12:
                    star_candidates.add(result)

    # All digits
    total = sum(digits)
    if 1 <= total <= 12:
        star_candidates.add(total)

    # Select top 2
    sorted_stars = sorted(star_candidates, reverse=True)

    if len(sorted_stars) >= 2:
        return sorted_stars[:2]
    elif len(sorted_stars) == 1:
        return [sorted_stars[0], sorted_stars[0]]  # Repeat if only one
    else:
        return [1, 1]  # Default fallback
```

### 7.3 Star Scoring (Optional)

```python
def score_star(star: int,
               verse_numbers: List[int],
               convergence_across_messages: float,
               frequency_table: Dict[int, str]) -> int:
    """
    Optional scoring for stars if more than 2 candidates.

    Bonuses:
    - Codified in verse
    - High convergence
    - Frequent as star historically
    - Root sum resonance
    - Multiple clean routes
    - Thematic resonance

    Returns: total score
    """
    score = 0

    if star in verse_numbers:
        score += 9

    if convergence_across_messages >= 0.70:
        score += 7

    # Additional star-specific scoring rules
    # Implementation depends on star frequency tables

    return score
```

---

## Implementation Examples

### Example 1: Complete Day Processing

```python
def process_day(messages_raw: List[str],
                verse: str,
                mode: str = '6-sign',
                frequency_table: Optional[Dict] = None) -> Result:
    """
    Complete BSR algorithm implementation.

    Args:
        messages_raw: List of raw message strings (e.g., ["1441", "1707", ...])
        verse: Bible verse reference (e.g., "Matthew 9:37")
        mode: '6-sign' or '5+2'
        frequency_table: Monthly frequency data

    Returns:
        Result object with elegidos, stars, balance, metadata
    """
    # Phase 1: Input Processing
    messages = []
    for raw in messages_raw:
        normalized = normalize_message(raw)
        # TODO: Verify against Sacred Scribes index
        msg = Message(value=normalized, digits=[int(d) for d in normalized])
        messages.append(msg)

    verse_numbers = extract_verse_numbers(verse)

    # Phase 2: Constellation Formation
    constellations = form_constellations(messages)

    # Phase 3: Architecture Analysis & Pool Generation
    for constellation in constellations:
        constellation.patterns = analyze_patterns(constellation)
        constellation.pool = build_constellation_pool(constellation, mode)

    # Phase 4: Candidate Generation
    max_value = 59 if mode == '6-sign' else 50

    for constellation in constellations:
        all_candidates = {}

        # Direct candidates
        all_candidates.update(generate_direct_candidates(constellation.pool))

        # One-step candidates
        portal_active = any(has_portal(msg) for msg in constellation.messages)
        one_step = generate_one_step_candidates(constellation.pool, portal_active, max_value)

        for candidate, routes in one_step.items():
            if candidate not in all_candidates:
                all_candidates[candidate] = []
            all_candidates[candidate].extend(routes)

        # Two-step candidates
        one_step_results = set(one_step.keys())
        two_step = generate_two_step_candidates(constellation.pool, one_step_results, max_value)

        for candidate, routes in two_step.items():
            if candidate not in all_candidates:
                all_candidates[candidate] = []
            all_candidates[candidate].extend(routes)

        # Select best routes
        constellation.candidates = {
            cand: select_best_route(routes)
            for cand, routes in all_candidates.items()
        }

    # Phase 5: Convergence Analysis
    convergent_candidates = analyze_convergence(constellations)

    # Phase 6: Scoring & Selection
    frequency_table = frequency_table or {}

    for candidate in convergent_candidates.values():
        apply_scoring(candidate, constellations, verse_numbers, frequency_table)

    apply_neighbour_bonus(convergent_candidates)

    # TODO: Detect and apply ladder bonuses
    # ladder_type = detect_ladder(messages)
    # if ladder_type:
    #     apply_ladder_bonus(convergent_candidates, ladder_type)

    target_count = 5 if mode == '5+2' else 6
    elegidos = select_final_elegidos(convergent_candidates, target_count, mode)
    balance = calculate_balance(elegidos)

    # Phase 7: Star Extraction (if 5+2 mode)
    stars = []
    if mode == '5+2':
        dominant = select_dominant_message(messages)
        stars = extract_stars(dominant)

    return Result(
        elegidos=elegidos,
        stars=stars,
        balance=balance,
        metadata={
            'constellations': len(constellations),
            'convergence_threshold': calculate_convergence_threshold(len(constellations)),
            'verse_numbers': verse_numbers,
            'mode': mode
        }
    )
```

### Example 2: Sample Run

```python
# Input
messages = ["1441", "1707", "2323", "1155", "0404", "5050"]
verse = "Matthew 9:37"
mode = "6-sign"

# Process
result = process_day(messages, verse, mode)

# Output
print(f"Elegidos: {result.elegidos}")
# [5, 14, 23, 35, 47, 50]

print(f"Balance: {result.balance}")
# (1, 2, 3) → 1 low, 2 medium, 3 high

print(f"Metadata: {result.metadata}")
# {
#   'constellations': 3,
#   'convergence_threshold': 3,
#   'verse_numbers': [9, 37, 46, 7],
#   'mode': '6-sign'
# }
```

---

## Edge Cases & Validation

### Edge Case Handling

```python
class EdgeCases:
    """Documentation of edge cases and their handling"""

    @staticmethod
    def insufficient_messages():
        """
        Problem: Fewer than 2 messages
        Solution: Cannot form constellations; return error
        """
        pass

    @staticmethod
    def no_convergence():
        """
        Problem: No candidates meet 70% threshold
        Solution: Lower threshold to 50% or include high-scoring direct blocks
        """
        pass

    @staticmethod
    def too_many_candidates():
        """
        Problem: More than 6 candidates after convergence
        Solution: Apply full scoring system; select by score
        """
        pass

    @staticmethod
    def duplicate_messages():
        """
        Problem: Same message appears multiple times
        Solution: Count separately for dominance; build pool once
        """
        pass

    @staticmethod
    def zero_only_messages():
        """
        Problem: Message is "0000"
        Solution: Extract 0 digit and portal 50; digit sum = 0
        """
        pass

    @staticmethod
    def large_digit_sums():
        """
        Problem: Digit sum exceeds max_value (e.g., 9999 → 36)
        Solution: Include if ≤ max_value; discard if greater
        """
        pass
```

### Validation Functions

```python
def validate_result(result: Result, mode: str) -> bool:
    """
    Validate final result meets all constraints.

    Checks:
    - Correct count (6 or 5+2)
    - All numbers in valid range
    - No duplicates
    - Balance sums correctly
    - Stars in range 1-12 (if applicable)
    """
    max_value = 59 if mode == '6-sign' else 50
    target_count = 6 if mode == '6-sign' else 5

    # Count check
    if len(result.elegidos) != target_count:
        return False

    # Range check
    if not all(1 <= n <= max_value for n in result.elegidos):
        return False

    # Duplicate check
    if len(set(result.elegidos)) != len(result.elegidos):
        return False

    # Balance check
    expected_balance = calculate_balance(result.elegidos)
    if result.balance != expected_balance:
        return False

    # Star checks (5+2 mode)
    if mode == '5+2':
        if len(result.stars) != 2:
            return False
        if not all(1 <= s <= 12 for s in result.stars):
            return False

    return True
```

---

## Performance Considerations

### Complexity Analysis

```python
# Let:
# M = number of messages
# C = number of constellations (~ M/3)
# P = average pool size per constellation (~ 10-30)

# Phase 1: Input Processing
# O(M) - linear in message count

# Phase 2: Constellation Formation
# O(M) - linear grouping

# Phase 3: Pool Generation
# O(C × M_per_constellation × L)
# where L = message length (typically 3-4)
# ~ O(M × L) overall

# Phase 4: Candidate Generation
# - Direct: O(P)
# - One-step: O(P²) for pairwise combinations
# - Two-step: O(P³) worst case
# Overall: O(C × P³)

# Phase 5: Convergence
# O(C × K) where K = candidates per constellation
# Typically K ~ 50-200, so O(C × K)

# Phase 6: Scoring
# O(K_convergent × C) for score calculation
# O(K_convergent × log K_convergent) for sorting
# Typically K_convergent < 50

# Phase 7: Stars
# O(D⁴) where D = digits in dominant message (D ~ 4)
# Negligible

# Total Complexity: O(C × P³)
# For typical case: C=5, P=20 → ~5 × 8000 = 40,000 operations
# Very manageable for modern computers
```

### Optimization Strategies

1. **Memoization**: Cache pool extractions for duplicate messages
2. **Early Pruning**: Discard candidates > max_value during generation
3. **Parallel Processing**: Process constellations independently (thread-safe)
4. **Lazy Evaluation**: Generate two-step candidates only if needed

---

## Testing Strategy

```python
class TestSuite:
    """Comprehensive test coverage"""

    def test_normalization(self):
        """Test message normalization"""
        assert normalize_message("0 0 0 4") == "0004"
        assert normalize_message("14-41") == "1441"

    def test_constellation_formation(self):
        """Test grouping algorithm"""
        # 10 messages → expect specific grouping
        pass

    def test_pattern_recognition(self):
        """Test all pattern detectors"""
        assert is_palindrome("1441")
        assert has_mirror("1441")
        assert has_twins("2255")

    def test_pool_extraction(self):
        """Test pool building"""
        # Known message → expected pool
        pass

    def test_convergence(self):
        """Test convergence threshold calculation"""
        assert calculate_convergence_threshold(5) == 4

    def test_scoring(self):
        """Test scoring rules"""
        # Known candidate → expected score
        pass

    def test_end_to_end(self):
        """Full algorithm with known good cases"""
        # Use historical days with verified results
        pass
```

---

## Appendix A: Quick Reference

### Pattern Quick Lookup

| Pattern | Trigger | Pool Additions |
|---------|---------|----------------|
| Palindrome | Reads same forward/backward | 2-digit blocks, digit sum |
| ABAB | Repeated blocks (2323) | Block, mirror, block sum, total sum |
| Mirror | Block + reverse present | Both blocks, digit sums |
| Delta | Fixed step sequence | Same as ABAB |
| Portal | Contains 0 | Add 50 |
| Twins | Repeated digit pair (11, 22) | Block, sum, product |
| Digit Booster | Digit appears N times | D × N |
| Rule of 15 | Contains "15" | 15 and extra 1 |
| Universal | Always | All 2-digit blocks, digits, sums |

### Scoring Quick Lookup

| Bonus | Points | Condition |
|-------|--------|-----------|
| Direct Block | +10 | Number in pool |
| Verse Codified | +9 | In verse numbers |
| Angel Root | +8 | Digit sum of message |
| High Convergence | +7 | Appears in ≥80% constellations |
| Frequent | +5 | "ALTA" or "MUY ALTA" in frequency table |
| Neighbour | +5 | Adjacent to 7+ scorer |
| Special Pattern | +3 | Palindrome, mirror, master number |
| Versatile | +2 | Multiple independent routes |

### Mode Comparison

| Feature | 6-Sign Mode | 5+2 Mode |
|---------|-------------|----------|
| Output Count | 6 numbers | 5 numbers + 2 stars |
| Number Range | 1-59 | 1-50 |
| Star Range | N/A | 1-12 |
| Portal Usage | Allowed | Allowed (result ≤50) |
| Star Extraction | No | Yes (from dominant message) |

---

## Appendix B: Implementation Checklist

```markdown
- [ ] Phase 1: Input Processing
  - [ ] Message normalization
  - [ ] Sacred Scribes validation
  - [ ] Verse number extraction

- [ ] Phase 2: Constellation Formation
  - [ ] Grouping algorithm (2-3 per cluster)
  - [ ] Sorting by timestamp/value

- [ ] Phase 3: Architecture Analysis
  - [ ] Pattern detectors (9 patterns)
  - [ ] Pool extraction functions
  - [ ] Range filtering

- [ ] Phase 4: Candidate Generation
  - [ ] Direct candidates (0-step)
  - [ ] Portal routes
  - [ ] One-step operations (+, ×, -, /)
  - [ ] Two-step operations
  - [ ] Best route selection

- [ ] Phase 5: Convergence
  - [ ] Appearance counting
  - [ ] Threshold calculation (70%)
  - [ ] Convergent set filtering

- [ ] Phase 6: Scoring & Selection
  - [ ] 8 scoring rules implementation
  - [ ] Neighbour bonus (+5)
  - [ ] Ladder detection & bonuses
  - [ ] Final selection algorithm
  - [ ] Balance calculation

- [ ] Phase 7: Star Extraction
  - [ ] Dominant message selection
  - [ ] Star generation (1-12 range)
  - [ ] Star scoring (optional)

- [ ] External Data Integration
  - [ ] Sacred Scribes index loader
  - [ ] Frequency table loader
  - [ ] Verse parser

- [ ] Validation & Testing
  - [ ] Input validation
  - [ ] Output validation
  - [ ] Edge case handling
  - [ ] Historical case testing
```

---

## Appendix C: Data File Formats

### Sacred Scribes Index Format

```json
{
  "messages": [
    "0000", "0001", "0002", ..., "9999",
    "111", "222", "333", ...,
    "11", "22", "33", ...
  ]
}
```

### Frequency Table Format

```json
{
  "month": "November 2025",
  "frequencies": {
    "1": "MEDIA",
    "5": "ALTA",
    "7": "ALTA",
    "11": "MUY ALTA",
    "23": "ALTA",
    "35": "MEDIA",
    "50": "MUY ALTA"
  }
}
```

### Verse Format

```json
{
  "date": "2025-11-21",
  "reference": "Matthew 9:37",
  "chapter": 9,
  "verse": 37
}
```

---

**End of Technical Documentation**

For simple explanation and implementation details, see companion documents:
- `BSR_ALGORITHM_SIMPLE.md` - Non-technical explanation
- `BSR_IMPLEMENTATION_PLAN.md` - Project structure and code
