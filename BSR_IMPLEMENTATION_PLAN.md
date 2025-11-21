# BSR Implementation Plan
## Complete Backend + Frontend Design

**Version:** 1.0
**Date:** 2025-11-21
**Technology Stack:** Python (Flask) + HTML/CSS/JavaScript

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Technology Choices](#technology-choices)
3. [Project Structure](#project-structure)
4. [Backend Design](#backend-design)
5. [Frontend Design](#frontend-design)
6. [API Specification](#api-specification)
7. [Implementation Steps](#implementation-steps)
8. [Sample Code](#sample-code)
9. [Deployment Guide](#deployment-guide)
10. [Future Enhancements](#future-enhancements)

---

## Project Overview

### Goal
Build a minimum viable BSR decoding tool with:
- Clean Python backend implementing the full algorithm
- Simple web interface for non-technical users
- REST API for programmatic access
- Local deployment (no cloud required initially)

### Success Criteria
- ✓ User can paste messages and get elegidos in < 5 seconds
- ✓ Results show reasoning (how numbers were chosen)
- ✓ No technical knowledge required to use
- ✓ Algorithm matches specification exactly
- ✓ Can run on local machine with Python 3.8+

---

## Technology Choices

### Backend: Python 3.8+ with Flask

**Why Python?**
- Clear, readable code for algorithm logic
- Excellent for mathematical operations
- Flask is lightweight and simple
- Easy to deploy locally

**Key Libraries:**
```
flask==2.3.0
flask-cors==4.0.0
python-dateutil==2.8.2
pytest==7.4.0
```

### Frontend: Vanilla HTML/CSS/JavaScript

**Why Vanilla?**
- No build step required
- Works in any browser
- Easy to understand and modify
- Minimal dependencies

**Components:**
- Single-page application
- Clean, minimal UI
- Responsive design (works on mobile)

### Data Storage: JSON Files

**Why JSON?**
- Simple to read/write
- No database setup required
- Version controllable
- Easy to edit manually

**Data Files:**
- `sacred_scribes_index.json` - Valid angel numbers
- `frequency_tables/2025-11.json` - Monthly frequency data
- `verses/2025-11.json` - Daily verses (optional)

---

## Project Structure

```
bsr-decoder/
│
├── backend/
│   ├── __init__.py
│   ├── app.py                    # Flask application entry point
│   ├── config.py                 # Configuration settings
│   ├── requirements.txt          # Python dependencies
│   │
│   ├── core/                     # Core algorithm modules
│   │   ├── __init__.py
│   │   ├── models.py             # Data classes (Message, Constellation, etc.)
│   │   ├── input_processor.py   # Phase 1: Normalization & validation
│   │   ├── constellation.py     # Phase 2: Grouping
│   │   ├── patterns.py           # Phase 3: Pattern recognition
│   │   ├── pool_builder.py      # Phase 3: Pool extraction
│   │   ├── candidate_gen.py     # Phase 4: Candidate generation
│   │   ├── convergence.py       # Phase 5: Convergence analysis
│   │   ├── scoring.py            # Phase 6: Scoring system
│   │   ├── selector.py           # Phase 6: Final selection
│   │   ├── star_extractor.py    # Phase 7: Star extraction
│   │   └── bsr_engine.py        # Main orchestrator
│   │
│   ├── api/                      # API routes
│   │   ├── __init__.py
│   │   ├── decode.py             # POST /api/decode
│   │   ├── validate.py           # POST /api/validate
│   │   └── health.py             # GET /api/health
│   │
│   ├── utils/                    # Utility functions
│   │   ├── __init__.py
│   │   ├── validators.py         # Input validation
│   │   ├── formatters.py         # Output formatting
│   │   └── data_loader.py        # Load JSON data files
│   │
│   └── tests/                    # Test suite
│       ├── __init__.py
│       ├── test_patterns.py
│       ├── test_convergence.py
│       ├── test_scoring.py
│       ├── test_end_to_end.py
│       └── fixtures/             # Test data
│           └── sample_days.json
│
├── frontend/
│   ├── index.html                # Main page
│   ├── css/
│   │   ├── main.css              # Main stylesheet
│   │   └── responsive.css        # Mobile styles
│   ├── js/
│   │   ├── app.js                # Main application logic
│   │   ├── api.js                # API communication
│   │   ├── ui.js                 # UI updates
│   │   └── validator.js          # Client-side validation
│   └── assets/
│       └── logo.png              # Optional branding
│
├── data/                         # Reference data
│   ├── sacred_scribes_index.json
│   ├── frequency_tables/
│   │   ├── 2025-10.json
│   │   ├── 2025-11.json
│   │   └── template.json
│   └── verses/
│       └── 2025-11.json
│
├── docs/                         # Documentation
│   ├── BSR_ALGORITHM_TECHNICAL.md
│   ├── BSR_ALGORITHM_SIMPLE.md
│   ├── BSR_IMPLEMENTATION_PLAN.md (this file)
│   └── API_REFERENCE.md
│
├── scripts/                      # Utility scripts
│   ├── setup_data.py             # Initialize data files
│   ├── validate_data.py          # Check data integrity
│   └── run_tests.sh              # Test runner
│
├── .gitignore
├── README.md                     # Project readme
├── LICENSE
└── docker-compose.yml            # Optional: Docker deployment
```

---

## Backend Design

### Core Architecture

```
┌─────────────────────────────────────────┐
│         Flask Application               │
│  (app.py - Entry Point)                 │
└────────────────┬────────────────────────┘
                 │
    ┌────────────┴────────────┐
    │                         │
    ▼                         ▼
┌─────────────┐        ┌─────────────┐
│  API Routes │        │   Core      │
│             │        │  Algorithm  │
│ /decode     │───────>│   Engine    │
│ /validate   │        │             │
│ /health     │        │  (7 phases) │
└─────────────┘        └─────────────┘
                              │
                    ┌─────────┴─────────┐
                    │                   │
                    ▼                   ▼
            ┌─────────────┐     ┌─────────────┐
            │   Utils     │     │    Data     │
            │ (Validators)│     │   Loaders   │
            └─────────────┘     └─────────────┘
```

### Module Descriptions

#### `models.py` - Data Classes

```python
@dataclass
class Message:
    value: str
    digits: List[int]
    timestamp: Optional[datetime] = None

@dataclass
class Constellation:
    messages: List[Message]
    pool: Set[int]
    patterns: List[str]
    candidates: Dict[int, 'Route']

@dataclass
class Route:
    result: int
    steps: int
    operations: str
    pool_elements: List[int]
    route_type: str

@dataclass
class Candidate:
    value: int
    appearances: int
    best_route: Route
    score: int
    bonuses: Dict[str, int]

@dataclass
class Result:
    elegidos: List[int]
    stars: List[int]
    balance: Tuple[int, int, int]
    metadata: Dict[str, Any]
```

#### `bsr_engine.py` - Main Orchestrator

```python
class BSREngine:
    """Main algorithm orchestrator"""

    def __init__(self, config: Config):
        self.config = config
        self.input_processor = InputProcessor()
        self.constellation_builder = ConstellationBuilder()
        self.pool_builder = PoolBuilder()
        self.candidate_generator = CandidateGenerator()
        self.convergence_analyzer = ConvergenceAnalyzer()
        self.scorer = Scorer()
        self.selector = Selector()
        self.star_extractor = StarExtractor()

    def process(self,
                messages_raw: List[str],
                verse: Optional[str] = None,
                mode: str = '6-sign') -> Result:
        """
        Main processing pipeline.
        Orchestrates all 7 phases.
        """
        # Phase 1: Input Processing
        messages = self.input_processor.process(messages_raw)
        verse_numbers = self.input_processor.extract_verse(verse)

        # Phase 2: Constellation Formation
        constellations = self.constellation_builder.build(messages)

        # Phase 3: Architecture Analysis & Pool Generation
        for constellation in constellations:
            patterns = self.pool_builder.analyze_patterns(constellation)
            pool = self.pool_builder.build_pool(constellation, mode)
            constellation.patterns = patterns
            constellation.pool = pool

        # Phase 4: Candidate Generation
        for constellation in constellations:
            candidates = self.candidate_generator.generate(
                constellation.pool,
                mode
            )
            constellation.candidates = candidates

        # Phase 5: Convergence Analysis
        convergent = self.convergence_analyzer.analyze(constellations)

        # Phase 6: Scoring & Selection
        self.scorer.score_all(
            convergent,
            constellations,
            verse_numbers
        )
        elegidos = self.selector.select(
            convergent,
            target_count=5 if mode == '5+2' else 6,
            mode=mode
        )
        balance = self.selector.calculate_balance(elegidos)

        # Phase 7: Star Extraction
        stars = []
        if mode == '5+2':
            dominant = self.star_extractor.find_dominant(messages)
            stars = self.star_extractor.extract(dominant)

        return Result(
            elegidos=elegidos,
            stars=stars,
            balance=balance,
            metadata=self._build_metadata(constellations, verse_numbers)
        )

    def _build_metadata(self, constellations, verse_numbers):
        """Build metadata for debugging and transparency"""
        return {
            'constellation_count': len(constellations),
            'convergence_threshold': calculate_threshold(len(constellations)),
            'verse_numbers': verse_numbers,
            'timestamp': datetime.now().isoformat()
        }
```

#### `patterns.py` - Pattern Recognition

```python
class PatternDetector:
    """Detects all structural patterns in messages"""

    @staticmethod
    def is_palindrome(msg: Message) -> bool:
        return msg.value == msg.value[::-1]

    @staticmethod
    def has_abab(msg: Message) -> bool:
        if len(msg.value) == 4:
            return msg.value[0:2] == msg.value[2:4]
        return False

    @staticmethod
    def has_mirror(msg: Message) -> bool:
        value = msg.value
        for i in range(len(value) - 1):
            block = value[i:i+2]
            reverse = block[::-1]
            if reverse in value and block != reverse:
                return True
        return False

    # ... (all other pattern detectors)

class PatternExtractor:
    """Extracts pool numbers based on patterns"""

    @staticmethod
    def extract_palindrome(msg: Message, max_value: int) -> Set[int]:
        pool = set()
        for i in range(len(msg.value) - 1):
            block = int(msg.value[i:i+2])
            if block <= max_value:
                pool.add(block)
        digit_sum = sum(msg.digits)
        if digit_sum <= max_value:
            pool.add(digit_sum)
        return pool

    # ... (all other extractors)
```

### API Layer

#### `api/decode.py` - Main Endpoint

```python
from flask import Blueprint, request, jsonify
from backend.core.bsr_engine import BSREngine
from backend.utils.validators import validate_request

decode_bp = Blueprint('decode', __name__)
engine = BSREngine(config)

@decode_bp.route('/api/decode', methods=['POST'])
def decode():
    """
    Main decoding endpoint.

    Request Body:
    {
        "messages": ["1441", "1707", "2323"],
        "verse": "Matthew 9:37",
        "mode": "6-sign"
    }

    Response:
    {
        "success": true,
        "result": {
            "elegidos": [5, 14, 23, 35, 47, 50],
            "stars": [],
            "balance": [1, 2, 3],
            "metadata": {...}
        },
        "explanation": [...]
    }
    """
    try:
        # Validate request
        data = request.get_json()
        errors = validate_request(data)
        if errors:
            return jsonify({'success': False, 'errors': errors}), 400

        # Extract parameters
        messages = data.get('messages', [])
        verse = data.get('verse')
        mode = data.get('mode', '6-sign')

        # Process
        result = engine.process(messages, verse, mode)

        # Build explanation
        explanation = build_explanation(result)

        return jsonify({
            'success': True,
            'result': {
                'elegidos': result.elegidos,
                'stars': result.stars,
                'balance': result.balance,
                'metadata': result.metadata
            },
            'explanation': explanation
        }), 200

    except ValueError as e:
        return jsonify({'success': False, 'error': str(e)}), 400
    except Exception as e:
        return jsonify({'success': False, 'error': 'Internal server error'}), 500

def build_explanation(result: Result) -> List[Dict]:
    """Build human-readable explanation of results"""
    explanation = []

    for num in result.elegidos:
        # Find how this number was generated
        # Include route, score, bonuses
        explanation.append({
            'number': num,
            'route': '...',
            'score': '...',
            'bonuses': [...]
        })

    return explanation
```

---

## Frontend Design

### UI Layout

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  BSR Decoder                                    [Help]  │
│                                                         │
│  ┌───────────────────────────────────────────────────┐ │
│  │ Enter Your Messages (one per line)               │ │
│  │                                                   │ │
│  │ 1441                                              │ │
│  │ 1707                                              │ │
│  │ 2323                                              │ │
│  │ 1155                                              │ │
│  │                                                   │ │
│  └───────────────────────────────────────────────────┘ │
│                                                         │
│  Daily Verse (optional)                                 │
│  ┌───────────────────────────────────────────────────┐ │
│  │ Matthew 9:37                                      │ │
│  └───────────────────────────────────────────────────┘ │
│                                                         │
│  Mode: ● 6-sign (1-59)  ○ 5+2 (1-50 + stars)          │
│                                                         │
│  ┌─────────────────────────┐                           │
│  │   Generate Numbers      │                           │
│  └─────────────────────────┘                           │
│                                                         │
│  ───────────────────────────────────────────────────── │
│                                                         │
│  Your Chosen Numbers:                                   │
│                                                         │
│  ┌────┐  ┌────┐  ┌────┐  ┌────┐  ┌────┐  ┌────┐      │
│  │ 5  │  │ 14 │  │ 23 │  │ 35 │  │ 47 │  │ 50 │      │
│  └────┘  └────┘  └────┘  └────┘  └────┘  └────┘      │
│                                                         │
│  Balance: 1 low, 2 medium, 3 high                      │
│                                                         │
│  ───────────────────────────────────────────────────── │
│                                                         │
│  How These Were Chosen:                                 │
│                                                         │
│  • 50 (Portal from 1707 + 0404) - Score: 27           │
│    ↳ Direct portal, appeared in 4/4 groups             │
│                                                         │
│  • 23 (Direct from 2323) - Score: 25                  │
│    ↳ Direct block, convergent, historically common     │
│                                                         │
│  • 14 (Direct from 1441) - Score: 22                  │
│    ↳ Direct block, convergent                          │
│                                                         │
│  [Show detailed breakdown ▼]                           │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

### HTML Structure (`index.html`)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BSR Decoder</title>
    <link rel="stylesheet" href="/css/main.css">
    <link rel="stylesheet" href="/css/responsive.css">
</head>
<body>
    <div class="container">
        <header>
            <h1>BSR Number Decoder</h1>
            <button id="help-btn" class="help-btn">?</button>
        </header>

        <main>
            <!-- Input Section -->
            <section class="input-section">
                <label for="messages">Your Messages (one per line):</label>
                <textarea
                    id="messages"
                    rows="8"
                    placeholder="1441&#10;1707&#10;2323&#10;1155"
                ></textarea>

                <label for="verse">Daily Verse (optional):</label>
                <input
                    type="text"
                    id="verse"
                    placeholder="Matthew 9:37"
                />

                <div class="mode-selector">
                    <label>Mode:</label>
                    <label>
                        <input type="radio" name="mode" value="6-sign" checked>
                        6-sign (1-59)
                    </label>
                    <label>
                        <input type="radio" name="mode" value="5+2">
                        5+2 (1-50 + stars)
                    </label>
                </div>

                <button id="generate-btn" class="primary-btn">
                    Generate Numbers
                </button>

                <div id="error-message" class="error hidden"></div>
            </section>

            <!-- Results Section -->
            <section id="results-section" class="results-section hidden">
                <h2>Your Chosen Numbers:</h2>

                <div id="elegidos-display" class="number-grid">
                    <!-- Numbers will be inserted here -->
                </div>

                <div id="stars-display" class="stars hidden">
                    <h3>Stars:</h3>
                    <div class="star-grid">
                        <!-- Stars will be inserted here -->
                    </div>
                </div>

                <div id="balance-display" class="balance">
                    <!-- Balance info will be inserted here -->
                </div>

                <h3>How These Were Chosen:</h3>
                <div id="explanation" class="explanation">
                    <!-- Explanation will be inserted here -->
                </div>

                <button id="detailed-btn" class="secondary-btn">
                    Show Detailed Breakdown
                </button>

                <div id="detailed-breakdown" class="detailed hidden">
                    <!-- Detailed info will be inserted here -->
                </div>
            </section>
        </main>

        <footer>
            <p>BSR 6.0 System | Deterministic Algorithm</p>
        </footer>
    </div>

    <!-- Help Modal -->
    <div id="help-modal" class="modal hidden">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>How to Use</h2>
            <p>1. Enter the repeated numbers you saw during the day (one per line)</p>
            <p>2. Optionally add your daily Bible verse</p>
            <p>3. Choose your mode (6-sign or 5+2)</p>
            <p>4. Click "Generate Numbers"</p>
            <p>5. View your chosen numbers and explanation</p>
        </div>
    </div>

    <script src="/js/api.js"></script>
    <script src="/js/ui.js"></script>
    <script src="/js/validator.js"></script>
    <script src="/js/app.js"></script>
</body>
</html>
```

### CSS Styling (`css/main.css`)

```css
:root {
    --primary-color: #4A90E2;
    --secondary-color: #7B68EE;
    --success-color: #50C878;
    --error-color: #E74C3C;
    --bg-color: #F8F9FA;
    --text-color: #333;
    --border-color: #DDD;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: var(--bg-color);
    color: var(--text-color);
    line-height: 1.6;
}

.container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
}

h1 {
    color: var(--primary-color);
}

.help-btn {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: var(--secondary-color);
    color: white;
    border: none;
    font-size: 20px;
    cursor: pointer;
}

/* Input Section */
.input-section {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    margin-bottom: 30px;
}

label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
}

textarea, input[type="text"] {
    width: 100%;
    padding: 12px;
    border: 1px solid var(--border-color);
    border-radius: 5px;
    font-size: 14px;
    margin-bottom: 20px;
}

textarea {
    resize: vertical;
    font-family: monospace;
}

.mode-selector {
    margin-bottom: 20px;
}

.mode-selector label {
    display: inline-block;
    margin-right: 20px;
}

.primary-btn {
    width: 100%;
    padding: 15px;
    background: var(--primary-color);
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.3s;
}

.primary-btn:hover {
    background: #357ABD;
}

.primary-btn:disabled {
    background: #CCC;
    cursor: not-allowed;
}

/* Results Section */
.results-section {
    background: white;
    padding: 30px;
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.number-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
    gap: 15px;
    margin: 20px 0;
}

.number-card {
    background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
    color: white;
    padding: 20px;
    border-radius: 10px;
    text-align: center;
    font-size: 32px;
    font-weight: bold;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.star-grid {
    display: flex;
    gap: 15px;
    margin: 10px 0;
}

.star-card {
    background: gold;
    color: #333;
    padding: 15px 25px;
    border-radius: 50%;
    font-size: 24px;
    font-weight: bold;
    box-shadow: 0 4px 6px rgba(0,0,0,0.2);
}

.balance {
    background: var(--bg-color);
    padding: 15px;
    border-radius: 5px;
    margin: 20px 0;
}

.explanation {
    margin: 20px 0;
}

.explanation-item {
    background: var(--bg-color);
    padding: 15px;
    border-left: 4px solid var(--primary-color);
    margin-bottom: 10px;
    border-radius: 3px;
}

.explanation-item .number {
    font-size: 24px;
    font-weight: bold;
    color: var(--primary-color);
}

.explanation-item .route {
    color: #666;
    font-size: 14px;
    margin: 5px 0;
}

.explanation-item .score {
    color: var(--success-color);
    font-weight: 600;
}

/* Utility Classes */
.hidden {
    display: none;
}

.error {
    background: #FFEBEE;
    color: var(--error-color);
    padding: 15px;
    border-radius: 5px;
    margin-top: 15px;
}

.loading {
    text-align: center;
    padding: 40px;
}

.spinner {
    border: 4px solid #f3f3f3;
    border-top: 4px solid var(--primary-color);
    border-radius: 50%;
    width: 40px;
    height: 40px;
    animation: spin 1s linear infinite;
    margin: 0 auto;
}

@keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

/* Modal */
.modal {
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.5);
}

.modal-content {
    background: white;
    margin: 10% auto;
    padding: 30px;
    width: 80%;
    max-width: 600px;
    border-radius: 10px;
    position: relative;
}

.close {
    position: absolute;
    right: 20px;
    top: 15px;
    font-size: 30px;
    cursor: pointer;
}
```

### JavaScript (`js/app.js`)

```javascript
// Main application logic

document.addEventListener('DOMContentLoaded', function() {
    const generateBtn = document.getElementById('generate-btn');
    const messagesInput = document.getElementById('messages');
    const verseInput = document.getElementById('verse');
    const modeInputs = document.querySelectorAll('input[name="mode"]');
    const resultsSection = document.getElementById('results-section');
    const errorMessage = document.getElementById('error-message');
    const helpBtn = document.getElementById('help-btn');
    const helpModal = document.getElementById('help-modal');

    // Generate button click
    generateBtn.addEventListener('click', async function() {
        // Clear previous errors
        errorMessage.classList.add('hidden');
        resultsSection.classList.add('hidden');

        // Get input values
        const messagesText = messagesInput.value.trim();
        const verse = verseInput.value.trim();
        const mode = document.querySelector('input[name="mode"]:checked').value;

        // Validate inputs
        const messages = messagesText.split('\n').map(m => m.trim()).filter(m => m);
        const errors = validateInput(messages, verse, mode);

        if (errors.length > 0) {
            showError(errors.join('<br>'));
            return;
        }

        // Show loading
        generateBtn.disabled = true;
        generateBtn.textContent = 'Processing...';

        try {
            // Call API
            const result = await decodeMessages(messages, verse, mode);

            // Display results
            displayResults(result);

            // Scroll to results
            resultsSection.scrollIntoView({ behavior: 'smooth' });

        } catch (error) {
            showError('Error: ' + error.message);
        } finally {
            generateBtn.disabled = false;
            generateBtn.textContent = 'Generate Numbers';
        }
    });

    // Help button
    helpBtn.addEventListener('click', function() {
        helpModal.classList.remove('hidden');
    });

    // Close modal
    document.querySelector('.close').addEventListener('click', function() {
        helpModal.classList.add('hidden');
    });

    // Close modal on outside click
    window.addEventListener('click', function(event) {
        if (event.target === helpModal) {
            helpModal.classList.add('hidden');
        }
    });
});

function showError(message) {
    const errorDiv = document.getElementById('error-message');
    errorDiv.innerHTML = message;
    errorDiv.classList.remove('hidden');
}

function displayResults(result) {
    const resultsSection = document.getElementById('results-section');
    const elegidosDisplay = document.getElementById('elegidos-display');
    const starsDisplay = document.getElementById('stars-display');
    const balanceDisplay = document.getElementById('balance-display');
    const explanationDiv = document.getElementById('explanation');

    // Display elegidos
    elegidosDisplay.innerHTML = result.elegidos.map(num =>
        `<div class="number-card">${num}</div>`
    ).join('');

    // Display stars (if 5+2 mode)
    if (result.stars && result.stars.length > 0) {
        starsDisplay.classList.remove('hidden');
        starsDisplay.querySelector('.star-grid').innerHTML = result.stars.map(star =>
            `<div class="star-card">★ ${star}</div>`
        ).join('');
    } else {
        starsDisplay.classList.add('hidden');
    }

    // Display balance
    const [low, medium, high] = result.balance;
    balanceDisplay.innerHTML = `
        <strong>Balance:</strong>
        ${low} low (1-9),
        ${medium} medium (10-29),
        ${high} high (30-59)
    `;

    // Display explanation
    if (result.explanation && result.explanation.length > 0) {
        explanationDiv.innerHTML = result.explanation.map(item => `
            <div class="explanation-item">
                <div class="number">${item.number}</div>
                <div class="route">${item.route}</div>
                <div class="score">Score: ${item.score}</div>
                ${item.bonuses && item.bonuses.length > 0 ? `
                    <div class="bonuses">
                        Bonuses: ${item.bonuses.join(', ')}
                    </div>
                ` : ''}
            </div>
        `).join('');
    }

    resultsSection.classList.remove('hidden');
}
```

### JavaScript (`js/api.js`)

```javascript
// API communication

const API_BASE_URL = 'http://localhost:5000';

async function decodeMessages(messages, verse, mode) {
    const response = await fetch(`${API_BASE_URL}/api/decode`, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify({
            messages: messages,
            verse: verse || null,
            mode: mode
        })
    });

    if (!response.ok) {
        const error = await response.json();
        throw new Error(error.error || 'Request failed');
    }

    const data = await response.json();

    if (!data.success) {
        throw new Error(data.error || 'Unknown error');
    }

    return {
        elegidos: data.result.elegidos,
        stars: data.result.stars || [],
        balance: data.result.balance,
        explanation: data.explanation || [],
        metadata: data.result.metadata
    };
}

async function validateMessages(messages) {
    const response = await fetch(`${API_BASE_URL}/api/validate`, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify({
            messages: messages
        })
    });

    const data = await response.json();
    return data.valid;
}

async function checkHealth() {
    const response = await fetch(`${API_BASE_URL}/api/health`);
    const data = await response.json();
    return data.status === 'ok';
}
```

---

## API Specification

### Endpoints

#### 1. POST `/api/decode`

**Description:** Main decoding endpoint

**Request:**
```json
{
    "messages": ["1441", "1707", "2323", "1155"],
    "verse": "Matthew 9:37",
    "mode": "6-sign"
}
```

**Response (Success):**
```json
{
    "success": true,
    "result": {
        "elegidos": [5, 14, 23, 35, 47, 50],
        "stars": [],
        "balance": [1, 2, 3],
        "metadata": {
            "constellation_count": 2,
            "convergence_threshold": 2,
            "verse_numbers": [9, 37, 46, 28],
            "timestamp": "2025-11-21T10:30:00"
        }
    },
    "explanation": [
        {
            "number": 50,
            "route": "Portal from 1707",
            "score": 27,
            "bonuses": ["portal", "convergent", "frequent"]
        },
        ...
    ]
}
```

**Response (Error):**
```json
{
    "success": false,
    "error": "Invalid message format",
    "errors": [
        "Message '9' is too short (minimum 2 digits)",
        "Message '3666' not found in Sacred Scribes index"
    ]
}
```

#### 2. POST `/api/validate`

**Description:** Validate messages without processing

**Request:**
```json
{
    "messages": ["1441", "1707", "3666"]
}
```

**Response:**
```json
{
    "valid": false,
    "errors": [
        "Message '3666' not found in Sacred Scribes index"
    ]
}
```

#### 3. GET `/api/health`

**Description:** Health check

**Response:**
```json
{
    "status": "ok",
    "version": "1.0.0",
    "timestamp": "2025-11-21T10:30:00"
}
```

---

## Implementation Steps

### Phase 1: Backend Core (Weeks 1-2)

1. **Setup project structure**
   ```bash
   mkdir bsr-decoder
   cd bsr-decoder
   python -m venv venv
   source venv/bin/activate
   pip install flask flask-cors pytest
   ```

2. **Implement data models** (`models.py`)
   - Message, Constellation, Route, Candidate, Result classes

3. **Implement Phase 1-2** (Input + Constellation)
   - `input_processor.py`
   - `constellation.py`
   - Write unit tests

4. **Implement Phase 3** (Patterns + Pools)
   - `patterns.py`
   - `pool_builder.py`
   - Write tests for each pattern

5. **Implement Phase 4** (Candidate Generation)
   - `candidate_gen.py`
   - Test 0-step, 1-step, 2-step generation

### Phase 2: Algorithm Completion (Week 3)

6. **Implement Phase 5** (Convergence)
   - `convergence.py`
   - Test with various constellation counts

7. **Implement Phase 6** (Scoring + Selection)
   - `scoring.py`
   - `selector.py`
   - Test scoring rules and tiebreakers

8. **Implement Phase 7** (Stars)
   - `star_extractor.py`
   - Test dominant message selection

9. **Integrate into BSREngine**
   - `bsr_engine.py`
   - End-to-end tests with known cases

### Phase 3: API Layer (Week 4)

10. **Build Flask app**
    - `app.py`
    - Configure CORS

11. **Implement API endpoints**
    - `/api/decode`
    - `/api/validate`
    - `/api/health`

12. **Add data loaders**
    - Load Sacred Scribes index
    - Load frequency tables
    - Parse verses

### Phase 4: Frontend (Week 5)

13. **Build HTML structure**
    - `index.html`
    - Form inputs, results display

14. **Add CSS styling**
    - `main.css`
    - Make it pretty and responsive

15. **Implement JavaScript**
    - `app.js` - Main logic
    - `api.js` - API calls
    - `ui.js` - UI updates
    - `validator.js` - Client validation

### Phase 5: Testing & Deployment (Week 6)

16. **Comprehensive testing**
    - Unit tests for all modules
    - Integration tests
    - End-to-end tests with historical data

17. **Documentation**
    - API reference
    - User guide
    - Developer setup guide

18. **Deployment**
    - Local deployment instructions
    - Optional: Docker container
    - Optional: Cloud deployment (Heroku, AWS, etc.)

---

## Sample Code

See backend samples in previous sections. For complete implementation:

```bash
# Clone repository
git clone https://github.com/yourusername/bsr-decoder.git
cd bsr-decoder

# Setup backend
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Run tests
pytest

# Start server
python app.py

# In another terminal, serve frontend
cd frontend
python -m http.server 8000

# Open browser to http://localhost:8000
```

---

## Deployment Guide

### Local Development

```bash
# Terminal 1: Backend
cd backend
source venv/bin/activate
flask run --port=5000

# Terminal 2: Frontend
cd frontend
python -m http.server 8000
```

### Docker Deployment

```dockerfile
# Dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY backend/requirements.txt .
RUN pip install -r requirements.txt

COPY backend/ ./backend/
COPY frontend/ ./frontend/
COPY data/ ./data/

EXPOSE 5000

CMD ["python", "backend/app.py"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  bsr-backend:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - ./data:/app/data
    environment:
      - FLASK_ENV=production
```

### Cloud Deployment (Heroku)

```bash
# Install Heroku CLI
heroku login
heroku create bsr-decoder

# Add Procfile
echo "web: python backend/app.py" > Procfile

# Deploy
git push heroku main
```

---

## Future Enhancements

### Phase 2 Features:

1. **Historical Data Storage**
   - Save all processed days to database
   - View past results
   - Trend analysis

2. **Batch Processing**
   - Upload multiple days at once
   - Export to CSV/Excel

3. **Advanced Analytics**
   - Frequency charts
   - Balance distribution graphs
   - Convergence visualizations

4. **User Accounts**
   - Save personal history
   - Custom frequency tables
   - Favorite numbers

5. **Mobile App**
   - Native iOS/Android app
   - Push notifications for daily processing

6. **API Enhancements**
   - GraphQL endpoint
   - Webhooks
   - Rate limiting

7. **AI Integration**
   - Predict likely elegidos before processing
   - Anomaly detection
   - Pattern discovery

---

## Testing Strategy

### Unit Tests

```python
# tests/test_patterns.py
import pytest
from backend.core.models import Message
from backend.core.patterns import PatternDetector, PatternExtractor

def test_palindrome_detection():
    msg = Message(value="1441", digits=[1,4,4,1])
    assert PatternDetector.is_palindrome(msg) == True

def test_palindrome_extraction():
    msg = Message(value="1441", digits=[1,4,4,1])
    pool = PatternExtractor.extract_palindrome(msg, max_value=59)
    assert 14 in pool
    assert 44 in pool
    assert 41 in pool
    assert 10 in pool  # digit sum

def test_mirror_detection():
    msg = Message(value="1441", digits=[1,4,4,1])
    assert PatternDetector.has_mirror(msg) == True

# ... more tests
```

### Integration Tests

```python
# tests/test_end_to_end.py
import pytest
from backend.core.bsr_engine import BSREngine
from backend.config import Config

def test_known_day_1():
    """Test against known good result from historical data"""
    engine = BSREngine(Config())

    messages = ["1441", "1707", "2323", "1155"]
    verse = "Matthew 9:37"
    mode = "6-sign"

    result = engine.process(messages, verse, mode)

    # Expected from historical verification
    expected_elegidos = [5, 14, 23, 35, 47, 50]

    assert result.elegidos == expected_elegidos
    assert len(result.elegidos) == 6
    assert all(1 <= n <= 59 for n in result.elegidos)
```

---

## Conclusion

This implementation plan provides:

✓ **Complete backend** with modular Python code
✓ **Simple frontend** with clean UI
✓ **REST API** for programmatic access
✓ **Local deployment** ready in minutes
✓ **Extensible architecture** for future features

**Next Steps:**
1. Follow implementation phases
2. Test against historical data
3. Deploy locally
4. Gather user feedback
5. Iterate and improve

**Repository Structure:** Ready for GitHub with proper documentation

**Time Estimate:** 6 weeks for MVP (1 developer)

**Stack Complexity:** Low (Flask + Vanilla JS = minimal dependencies)

---

**For questions or contributions, see:**
- Technical docs: `BSR_ALGORITHM_TECHNICAL.md`
- Simple explanation: `BSR_ALGORITHM_SIMPLE.md`
- This implementation plan: `BSR_IMPLEMENTATION_PLAN.md`

**License:** Specify your preferred license (MIT, Apache, proprietary, etc.)
