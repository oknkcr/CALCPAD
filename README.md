# CalcPad Pro

> A **Mathcad-style engineering calculation workspace** built as a single HTML file — no installation, no dependencies, runs entirely in your browser.

![CalcPad Pro](https://img.shields.io/badge/version-5.0-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![HTML](https://img.shields.io/badge/built%20with-HTML%2FJS-orange)

---
---

APP LINK: [GitHub Pages](https://oknkcr.github.io/CALCPAD/)

---
## ✨ Features

### 🧮 Calculation Engine
- **Live expression evaluation** — results update instantly as you type
- **Variable assignment** with cascade recalculation — change one value and all dependents update automatically
- **2-pass evaluation** — use variables before they're defined; order on canvas doesn't matter
- **Forward references** — `area = PI * r^2` works even if `r` is defined below it
- **Global variables** — mark any variable as 🌍 Global to share it across all pages

### 📐 Block Types
| Block | Description |
|-------|-------------|
| `:= Variable` | Assign a named value (`r = 5`, `F = m * a`) |
| `= Expression` | Evaluate any formula (`2 * PI * r`) |
| `✎ Text` | Free-form annotation |
| `§ Section` | Section header / divider |
| `∿ Plot` | Function graph with configurable x-range |
| `⊞ Matrix` | Matrix input with named variable, sum, trace, determinant |
| `? Condition` | If/then/else logic with optional variable assignment |
| `⊕ Subpage` | Hierarchical calculation pages |
| `⬚ Group Box` | Visual grouping of related blocks |

### 📋 Formula Snippet Library
- **30+ built-in snippets** organized by category: Geometry, Trigonometry, Physics, Engineering, Statistics, Finance
- **Personal snippet library** — save your own formulas with a single click (📌 pin button on any block)
- Snippets persist across sessions via `localStorage`

### 🖱 Canvas Navigation
- **Free-form drag & drop** canvas — place blocks anywhere
- **Middle-click** → opens a 3-tab context menu at cursor position:
  - **Block** — add any block type + variable browser
  - **📐 Snippet** — insert built-in or personal formula snippets
  - **f(x)** — quick function buttons (√, sin, cos, log, π, Σ…)
- **Double-click** on empty canvas → creates an Expression block at that position
- **Alt + drag** or **right-drag** → pan the canvas
- **Scroll wheel** → zoom in/out centered on cursor
- **⊞ Fit View** button / `Home` key → smoothly animates to show all blocks

### 💾 Save & Load
- **Save to `.calcpad` file** (`Ctrl+S`) — portable JSON format
- **Open `.calcpad` file** — restores complete workspace
- **Autosave** to `localStorage` — prompts to restore last session on startup
- **TXT export** — plain text summary of all variables and results

### 🔍 Search
- Search blocks by ID, variable name, or text content
- Filter buttons: All / #ID / Variable / Text
- Click result → smooth zoom-and-pan to that block with flash highlight

### 📋 Copy Results
- Hover over any result row → **⎘ copy button** appears
- Copies the raw numeric value to clipboard for pasting into other documents

---

## 🚀 Getting Started

1. **Download** `calcpad.html`
2. **Open** it in any modern browser (Chrome, Firefox, Edge, Safari)
3. That's it — no server, no build step, no dependencies

---

## 🎮 Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `F5` | Recalculate everything |
| `Home` | Fit all blocks into view |
| `Ctrl+S` | Save to `.calcpad` file |
| `Alt+Delete` | Delete selected block |
| `Arrow keys` | Nudge selected block |
| `Alt+Backspace` | Go back to parent page |
| `Escape` | Deselect / close menus |
| `Middle click` | Open context menu at cursor |
| `Double click` (canvas) | Create expression block at cursor |
| `Alt + drag` | Pan the canvas |
| `Scroll` | Zoom in/out |

---

## 🧠 Math Engine

CalcPad evaluates expressions using JavaScript's native math with an extended function set:

### Built-in Functions
```
sqrt(x)   abs(x)    sin(x)    cos(x)    tan(x)
asin(x)   acos(x)   atan(x)   atan2(y,x)
log(x)    ln(x)     exp(x)    pow(x,n)
floor(x)  ceil(x)   round(x)  sign(x)
deg(x)    fac(n)
sum(...)  avg(...)  norm(v)   dot(a,b)
max(...)  min(...)
```

### Constants
```
PI    E    PHI    SQRT2    INF
```

### Syntax
```
r = 5                     # variable assignment
area = PI * r^2           # uses ^ for exponentiation
v = [1, 2, 3, 4]         # vector / list literal
sum(v)                    # → 10
A[0]                      # first element of matrix/vector A
sin(deg(45))              # sin of 45 degrees
```

---

## 📁 Workspace Structure

```
Workspace
├── Root Page
│   ├── Blocks (assign, expr, text, plot, matrix, cond, group)
│   └── Subpages
│       ├── Page 2
│       └── Page 3
└── Global Variables (shared across all pages)
```

Each page has its own local variable scope. Global variables (marked with 🌍) are accessible from every page.

---

## 💡 Usage Examples

### Basic Engineering Calculation
```
r = 0.05          # shaft radius [m]
L = 1.2           # length [m]
F = 5000          # axial force [N]
A = PI * r^2      # cross-section area
sigma = F / A     # stress [Pa]
```

### Conditional Logic with Variable Assignment
```
If:     sigma > 250e6
Then:   1            (FAIL)
Else:   0            (OK)
→ assign to: check
```

### Matrix / Vector Operations
```
Matrix named "loads": [1200, 850, 2100, 975]
sum(loads)   → 5125
avg(loads)   → 1281.25
max(loads)   → 2100
```

---

## 🗂 File Format

CalcPad saves workspaces as `.calcpad` files (JSON):

```json
{
  "version": 2,
  "savedAt": "2025-03-19T...",
  "title": "My Calculation",
  "pageIdCtr": 3,
  "blockCtr": 12,
  "pageStack": ["root"],
  "pages": {
    "root": {
      "id": "root",
      "title": "Main",
      "blocks": [
        {
          "id": 1, "type": "assign",
          "x": 60, "y": 80,
          "text": "r = 5",
          "isGlobal": false
        }
      ]
    }
  }
}
```

---

## 🗺 Roadmap

- [ ] Unit system support (SI, Imperial)
- [ ] PDF export with formatted equations
- [ ] Collaborative real-time editing
- [ ] Custom function definitions (`def f(x) = ...`)
- [ ] Chart types: bar, scatter, histogram
- [ ] Dark/light theme toggle
- [ ] Mobile touch support

---

## 🛠 Technical Notes

- **Single HTML file** — all CSS, JS, and markup in one file (~2300 lines)
- **No external dependencies** — pure vanilla JavaScript
- **Storage** — `localStorage` for autosave and personal snippets; `.calcpad` JSON files for portability
- **Evaluation** — uses `new Function()` for safe expression sandboxing with explicit scope injection
- **Canvas** — CSS `transform: translate + scale` for pan/zoom with 6000×5000px world space

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

*Built as a single-file engineering notepad. Inspired by Mathcad.*
