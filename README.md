# Precision Calculator

A clean, responsive **standard and scientific calculator** built as a single `index.html` file with HTML, Tailwind CSS, and vanilla JavaScript.

No frameworks, no build step, no dependencies to install — open the file and calculate.

> **The 3-minute challenge**  
> A complete standard & scientific calculator — hand-written expression engine, full keyboard support, responsive interface, and documentation — designed, committed, and shipped to GitHub in under three minutes.  
> No frameworks. No build step. No compromise on the details.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)](https://tailwindcss.com/)
[![Vanilla JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)](./LICENSE)
[![Built in under 3 minutes](https://img.shields.io/badge/built_in-under_3_minutes-d8ff4a?style=flat-square&labelColor=161910)](https://github.com/muhammadsami987123/precision-calculator)

---

## Overview

Precision Calculator is a small, focused web app for everyday arithmetic and scientific math. It pairs a calm, high-contrast interface with a hand-written expression engine, live result previews, full keyboard support, and clear error messages when a calculation cannot be completed.

Everything lives in one HTML file. The only external resources are the Tailwind CSS CDN and Google Fonts.

---

## Features

### Standard mode
- Addition, subtraction, multiplication, and division
- Decimal input and chained calculations
- Clear-all and backspace editing
- Live result preview while typing
- Unary negative input with the minus key

### Scientific mode
- Trigonometric functions: `sin`, `cos`, `tan`
- Degree / radian toggle, always visible in the display
- Powers with `xʸ`
- Square roots
- Parentheses for grouped expressions
- Base-10 logarithm (`log`) and natural logarithm (`ln`)
- Mathematical constants: `π` and `e`
- Implicit multiplication, e.g. `2π`, `2(3 + 4)`, `3sin(30)`

### Calculation engine
- Custom tokenizer and recursive-descent parser — **no `eval()`**
- Correct operator precedence and right-associative powers
- Automatic closing of unclosed parentheses when solving
- Results rounded to 12 significant digits and grouped for readability
- Scientific notation for very large or very small results
- Smart input handling: duplicate decimals are ignored, leading zeros are trimmed, and operators are replaced instead of stacked

### Interface and accessibility
- Fully responsive layout from small phones to wide desktops
- Live expression line with a muted result preview
- Keyboard-first workflow with visible focus states
- Touch targets of 44px or more
- `aria-live` alerts for errors and a screen-reader result announcement
- Reduced-motion support
- No tracking, no accounts, no network calls after assets load

---

## Error handling

The calculator fails gracefully instead of showing `NaN`, `Infinity`, or a blank screen.

| Situation | Message shown |
| --- | --- |
| Division by zero, including `5 / (3 - 3)` | `Cannot divide by zero.` |
| Square root of a negative number | `Square roots need a value of zero or more.` |
| `log` or `ln` of zero / a negative number | `Logarithms need a value greater than zero.` |
| `tan(90°)` and equivalent angles | `tan is undefined at this angle.` |
| Incomplete expression such as `2 +` | `Finish the expression and try again.` |
| Extra closing parenthesis | `There is an extra closing parenthesis.` |
| Non-real result | `This calculation has no real result.` |
| Result too large to represent | `The result is too large to display.` |
| Invalid character or function | A specific input error message |

After an error, press **Backspace** to correct the expression or **AC** / **Esc** to start over. Typing a number starts a fresh calculation.

---

## Tech stack

- **HTML5** — semantic structure, accessible controls
- **Tailwind CSS** (CDN) — layout, spacing, typography utilities
- **Vanilla JavaScript** — calculator state, tokenizer, parser, formatter, keyboard handling
- **Google Fonts** — Instrument Sans, Instrument Serif, JetBrains Mono

---

## Getting started

### Option 1 — Open directly

1. Clone the repository:
   ```bash
   git clone https://github.com/muhammadsami987123/precision-calculator.git
   cd precision-calculator
   ```
2. Open `index.html` in any modern browser.

That's it. There is no install, compile, or build step.

### Option 2 — Run a local server

A local server is optional, but useful for mobile testing on the same network.

```bash
# Python 3
python -m http.server 8000

# or Node.js
npx serve .
```

Then visit `http://localhost:8000`.

---

## Usage

1. Choose **Standard** or **Scientific** with the switch at the top of the calculator.
2. Tap the keypad or use your physical keyboard.
3. Press **Enter** or **=** to solve. The result is shown while typing, then confirmed on solve.
4. After solving, press an operator to continue from the result, or start typing a digit for a new calculation.
5. In Scientific mode, use the **DEG / RAD** key to change the angle unit used by `sin`, `cos`, and `tan`.

### Keyboard shortcuts

| Key | Action |
| --- | --- |
| `0` – `9` | Enter digits |
| `.` | Decimal point |
| `+`, `-`, `*`, `/`, `^` | Operators |
| `x` or `X` | Multiply |
| `(` and `)` | Parentheses |
| `Enter` or `=` | Solve |
| `Backspace` | Delete the last input |
| `Esc` or `Delete` | Clear everything |

Keyboard input works anywhere on the page and briefly highlights the matching on-screen key.

---

## Supported functions and operators

| Input | Meaning | Example |
| --- | --- | --- |
| `+` `-` `*` `/` | Basic arithmetic | `12 * 4` → `48` |
| `^` | Power (right-associative) | `2^3^2` → `512` |
| `sqrt(x)` | Square root | `sqrt(81)` → `9` |
| `sin(x)` `cos(x)` `tan(x)` | Trigonometry in DEG or RAD | `sin(30)` → `0.5` in DEG |
| `log(x)` | Base-10 logarithm | `log(1000)` → `3` |
| `ln(x)` | Natural logarithm | `ln(e)` → `1` |
| `π` | Pi | `2π` → `6.28318530718` |
| `e` | Euler's number | `ln(e)` → `1` |
| `( )` | Grouping | `(2 + 3) * 4` → `20` |

Implicit multiplication is supported, so `2(3 + 4)` is treated as `2 × (3 + 4)`, and `2sin(30)` as `2 × sin(30)`.

---

## Project structure

```text
precision-calculator/
├── index.html   # Complete application: markup, styles, calculation engine, UI
├── README.md    # Project documentation
└── LICENSE      # MIT License
```

The file is organized into distinct sections:

- **Head** — metadata, fonts, Tailwind configuration, and the design system in `<style>`
- **Markup** — header, introductory copy, calculator, footer
- **`#calc-core` script** — pure tokenizer, parser, evaluator, and number formatter
- **UI script** — state management, rendering, keyboard input, and mode switching

---

## Implementation notes

- **No `eval()`.** User input is tokenized and parsed by a small recursive-descent parser. This makes precedence explicit and keeps unsupported characters out of the evaluator.
- **Precedence.** Unary signs bind below powers, so `-2^2` evaluates to `-4`. Powers are right-associative, so `2^3^2` is `2^(3^2)`.
- **Precision.** Results are formatted to 12 significant digits with `Intl`-style grouping implemented manually. Floating-point artifacts such as `0.30000000000000004` display as `0.3`.
- **Trigonometry.** Degree input is converted to radians. Values within `1e-12` of zero are snapped to `0` so `cos(90°)` reads as `0`. The tangent function explicitly rejects angles where cosine is effectively zero.
- **Angle changes.** Switching DEG/RAD after a solved trigonometric expression recalculates the displayed result in the new unit.
- **Tailwind CDN.** The CDN build is used for a zero-setup, single-file project. For a production deployment with strict performance budgets, compile Tailwind ahead of time and replace the CDN script with a static stylesheet.

---

## Browser support

Tested on current versions of Chrome, Edge, Firefox, and Safari. Requires JavaScript and a browser with support for modern CSS grid and `dvh` units.

---

## License

Released under the [MIT License](./LICENSE).

Copyright © 2026 Muhammad Sami Asghar Mughal.

---

## Author

**Muhammad Sami** — Forward Deployed Engineer, AI Agent Engineer, Full-Stack Developer

- Portfolio: [muhammad-sami.vercel.app](https://muhammad-sami.vercel.app)
- GitHub: [@muhammadsami987123](https://github.com/muhammadsami987123)
- LinkedIn: [Muhammad Sami](https://www.linkedin.com/in/muhammad-sami-3aa6102b8/)
