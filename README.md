<div align="center">

# 🎨 GitHub Commit Graph Art

**Turn your GitHub contribution graph into a canvas.**  
Write words, draw patterns, and make your profile stand out — automatically.

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)
[![Stars](https://img.shields.io/github/stars/kushdeveloper68/github-graph-art?style=flat-square)](https://github.com/kushdeveloper68/github-graph-art/stargazers)

<br/>

![GitHub Graph Art Demo](https://ajmendez.github.io/assets/helloworld_finished.png)

*Example: "HELLO" written on a real GitHub contribution graph*

</div>

---

## 📖 Table of Contents

- [What Is This?](#-what-is-this)
- [How the GitHub Graph Works](#-how-the-github-graph-works)
- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [All Modes & Usage](#-all-modes--usage)
  - [Mode 1 — Random Commits](#mode-1--random-commits)
  - [Mode 2 — Text Art](#mode-2--text-art)
  - [Mode 3 — Built-in Patterns](#mode-3--built-in-patterns)
  - [Mode 4 — Custom Grid](#mode-4--custom-grid)
  - [Dry Run (Preview Mode)](#dry-run-preview-mode)
- [Intensity Levels](#-intensity-levels)
- [Supported Characters & Symbols](#-supported-characters--symbols)
- [Tips & Tricks](#-tips--tricks)
- [FAQ](#-faq)
- [Contributing](#-contributing)
- [Made With](#-made-with)
- [License](#-license)

---

## 🤔 What Is This?

Your GitHub profile shows a **contribution graph** — a 52-week × 7-day grid where each cell lights up green based on how many commits you made that day.

This tool **crafts commits with backdated timestamps** to paint that grid like a pixel display. You can:

- Scatter random commits to make your graph look busy and active
- **Spell out words** like `HELLO`, `COOL`, your name, or any message
- Draw geometric patterns (checkerboard, wave, stripes)
- Design your own custom pixel art

> **Note:** This is for fun / learning / portfolio aesthetics. The commits are real Git commits — they just have custom dates.

---

## 🔬 How the GitHub Graph Works

GitHub's contribution graph is a **52-column × 7-row** grid:

```
        Week 0  Week 1  Week 2  ...  Week 51
Sun  [  ░  ] [  ░  ] [  ░  ]       [  ░  ]
Mon  [  ░  ] [  ░  ] [  ░  ]       [  ░  ]
Tue  [  ░  ] [  ░  ] [  ░  ]       [  ░  ]
Wed  [  ░  ] [  ░  ] [  ░  ]       [  ░  ]
Thu  [  ░  ] [  ░  ] [  ░  ]       [  ░  ]
Fri  [  ░  ] [  ░  ] [  ░  ]       [  ░  ]
Sat  [  ░  ] [  ░  ] [  ░  ]       [  ░  ]
```

Each cell's shade is determined by **commit count that day**:

| Commits | Color |
|---------|-------|
| 0 | ⬜ Empty |
| 1–3 | 🟩 Light green |
| 4–9 | 🟩 Medium green |
| 10–19 | 🟩 Dark green |
| 20+ | 🟩 Darkest green |

This tool writes commits with `--date` overrides to place them precisely in any cell.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🎲 **Random fill** | Scatter N commits randomly across the past year |
| ✏️ **Text art** | Write words/phrases using a 5×7 pixel font |
| 🔷 **Built-in patterns** | Checkerboard, wave, diagonal stripes |
| 🖌️ **Custom grid** | Supply your own 7×52 intensity array |
| 🔍 **Dry run mode** | Preview your art in the terminal without touching Git |
| 🌈 **Intensity control** | Light / medium / heavy green per cell |
| 💬 **Terminal preview** | See a `█ / ░` ASCII preview before committing |
| 📦 **Push automation** | Automatically pushes to your remote after drawing |

---

## 📋 Prerequisites

Before you begin, make sure you have:

- **Node.js** v18 or later ([Download](https://nodejs.org))
- **npm** v8 or later (comes with Node)
- **Git** installed and configured on your machine
- A **GitHub account** with a repository to push to
- Your **SSH key or HTTPS token** set up so `git push` works without prompts

---

## 🚀 Installation

### Step 1 — Fork or clone this repo

```bash
# Clone the repo
git clone https://github.com/kushdeveloper68/github-graph-art.git
cd github-graph-art
```

### Step 2 — Create a dedicated GitHub repo

> ⚠️ **Use a fresh, empty repository** — not an existing project.  
> The script will spam commits and overwrite `data.json` constantly.

1. Go to [github.com/new](https://github.com/new)
2. Name it something like `github-graph-art` or `commit-art`
3. Make it **public** (private repos don't show on the contribution graph unless you enable it in settings)
4. **Don't** initialize with a README
5. Copy the remote URL

### Step 3 — Set your remote

```bash
git remote set-url origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
# or for SSH:
git remote set-url origin git@github.com:YOUR_USERNAME/YOUR_REPO.git
```

### Step 4 — Install dependencies

```bash
npm install
```

### Step 5 — Initialize the data file

```bash
echo '{"date":"init"}' > data.json
git add data.json
git commit -m "init"
git push -u origin main
```

---

## ⚡ Quick Start

Open `index.js` and uncomment **one mode** at the bottom of the file:

```js
// ─── CLI Entry Point ──────────────────────────────────────────────────────────

// 1️⃣  100 random commits scattered across the year
makeRandomCommits(100);

// 2️⃣  Write "HELLO" starting at week 5
// makeTextArt("HELLO", 5, "heavy", false);
```

Then run:

```bash
node index.js
```

---

## 🎛️ All Modes & Usage

### Mode 1 — Random Commits

Scatter commits randomly across the past year. Great for making your graph look naturally active.

```js
import { makeRandomCommits } from "./index.js";

// Scatter 200 commits randomly
makeRandomCommits(200);

// Dry run first to see what dates would be used
makeRandomCommits(200, true);
```

**Parameters:**

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `n` | number | — | Total number of commits to make |
| `dryRun` | boolean | `false` | If `true`, only prints dates — no commits made |

---

### Mode 2 — Text Art

Write a custom word or phrase onto your graph using a built-in 5×7 pixel font.

```js
import { makeTextArt } from "./index.js";

// Write "HI" starting at week 10 with heavy intensity
makeTextArt("HI", 10, "heavy");

// Write your name (dry run preview first)
makeTextArt("CODE", 0, "heavy", true);

// Combine two words side by side (each letter = 6 cols wide)
// "COOL" = 4 letters × 6 cols = 24 columns → start "CODE" at week 26
makeTextArt("COOL", 0, "heavy");
makeTextArt("CODE", 26, "heavy");
```

**Parameters:**

| Param | Type | Default | Description |
|-------|------|---------|-------------|
| `text` | string | — | The word/phrase to draw |
| `startWeek` | number | `0` | Which week column to begin (0–51) |
| `level` | string | `"heavy"` | Intensity: `"light"`, `"medium"`, or `"heavy"` |
| `dryRun` | boolean | `false` | Preview without committing |

**Planning your text position:**

- Each character is **5 columns** wide + **1 column** spacing = **6 columns per letter**
- The graph is **52 columns** wide = max ~8 letters
- Example: A 5-letter word = 30 columns → fits nicely starting at week 10

**Terminal preview output:**

```
✏️  Drawing text: "HI" starting at week 10

█░░░█ ░█░
█░░░█ ░█░
█░░░█ ░█░
█████ ░█░
█░░░█ ░█░
█░░░█ ░█░
█░░░█ ░█░
```

---

### Mode 3 — Built-in Patterns

Draw geometric patterns across the entire 52-week graph.

```js
import { makePattern } from "./index.js";

// Available patterns: "checkerboard", "wave", "stripes"
makePattern("wave");
makePattern("checkerboard");
makePattern("stripes");

// Dry run preview
makePattern("wave", true);
```

**Pattern descriptions:**

| Pattern | Description |
|---------|-------------|
| `checkerboard` | Alternating heavy/empty cells like a chess board |
| `wave` | Sinusoidal wave sweeping left to right |
| `stripes` | Diagonal stripes at 45° |

---

### Mode 4 — Custom Grid

Supply your own 7×52 intensity matrix for full pixel-art control.

```js
import { makeCustomGrid } from "./index.js";

// Each row = one day of the week (0=Sun, 6=Sat)
// Each column = one week
// Values: 0 = empty, 1 = light, 5 = medium, 15 = heavy

const myGrid = [
  [0,0,15,0,0, ...],   // Sunday
  [0,15,15,15,0, ...], // Monday
  [15,0,15,0,15, ...], // Tuesday
  [0,15,15,15,0, ...], // Wednesday
  [0,0,15,0,0, ...],   // Thursday
  [0,0,0,0,0, ...],    // Friday
  [0,0,0,0,0, ...],    // Saturday
];

makeCustomGrid(myGrid, false);
```

---

### Dry Run (Preview Mode)

Every function accepts a `dryRun` parameter. When `true`:

- Prints the ASCII terminal preview
- Prints all dates that *would* be used
- **Makes zero Git commits**

Always test with `dryRun: true` first:

```js
makeTextArt("HELLO", 0, "heavy", true);  // ← safe preview
makeTextArt("HELLO", 0, "heavy", false); // ← actually commits
```

---

## 🌈 Intensity Levels

Control how dark each cell appears on the graph:

```js
const INTENSITY = {
  none:   0,   // ⬜ empty cell
  light:  1,   // 🟩 barely visible
  medium: 5,   // 🟩 medium green
  heavy:  15,  // 🟩 darkest green
};
```

Use `"light"` intensity to create subtle outlines, or mix intensities in a custom grid for gradient effects.

---

## 🔤 Supported Characters & Symbols

The built-in pixel font currently supports:

| Category | Characters |
|----------|------------|
| Uppercase letters | `A–Z` |
| Digits | `0–3` (more coming soon) |
| Symbols | `!` `♥` (space) |

> **Can't see your character?** Unknown characters are silently skipped.  
> You can add your own glyphs to the `FONT` object in `index.js` — each is a 7×5 boolean grid. PRs for new characters are very welcome!

---

## 💡 Tips & Tricks

**1. Always dry run first**
```js
makeTextArt("HELLO", 0, "heavy", true); // preview
```

**2. Plan your layout with column math**
- 6 columns per character × number of chars = total width needed
- Graph = 52 columns wide
- Leave a few blank weeks on each edge for visual breathing room

**3. Combine modes**
```js
// Background random noise + text on top
await makeRandomCommits(50);
await makeTextArt("CODE", 20, "heavy");
```

**4. Wait a few minutes after pushing**
GitHub caches contribution graphs — your art usually appears within 5–10 minutes.

**5. Set your repo to public**
Private repo commits only show on the graph if you enable "Private contributions" in your GitHub settings at [github.com/settings/profile](https://github.com/settings/profile).

**6. Use a throwaway repo**
Point the remote at a dedicated art repo so it doesn't pollute a real project's history.

---

## ❓ FAQ

**Q: Will this hurt my GitHub account?**  
A: No. These are standard Git commits with custom `--date` metadata. GitHub treats them identically to any other commit.

**Q: My graph didn't change after running the script.**  
A: Check that (1) `git push` succeeded, (2) the repo is public, and (3) you've waited ~10 minutes for GitHub's cache to refresh.

**Q: Can I draw on a specific month/date range?**  
A: Yes — adjust `startWeek`. Week 0 is ~one year ago, week 51 is the current week. Count forward from week 0 to reach any month.

**Q: Can I erase the graph?**  
A: GitHub doesn't let you "un-count" commits easily. You'd need to delete the repository and recreate it, or use `git rebase` to remove the commits. Consider this a one-way operation.

**Q: The text is cut off on the right side.**  
A: Your word is wider than the remaining columns from `startWeek`. Lower `startWeek` or use a shorter word.

**Q: Can I write lowercase?**  
A: The script auto-uppercases your input. At 5×7 pixels, lowercase letters are very hard to distinguish — uppercase looks much cleaner on the graph grid.

---

## 🤝 Contributing

Contributions are warmly welcomed! Here's how to get involved:

1. **Fork** this repository
2. **Create** a feature branch: `git checkout -b feature/new-pattern`
3. **Commit** your changes with a clear message
4. **Push** and open a **Pull Request**

### Ideas for contributions

- [ ] Add more letters/digits to the `FONT` object
- [ ] Add more built-in patterns (spiral, cross, border)
- [ ] CLI argument parsing (`node index.js --text HELLO --week 5`)
- [ ] Interactive mode with prompts
- [ ] Week-position calculator / planning helper
- [ ] Digit completion (currently only 0–3 are defined)

Please keep PRs focused on a single feature/fix. Add a comment explaining what your pattern or glyph does.

---

## 🛠️ Made With

| Package | Purpose |
|---------|---------|
| [`simple-git`](https://www.npmjs.com/package/simple-git) | Programmatic Git operations (add, commit, push) |
| [`moment`](https://www.npmjs.com/package/moment) | Date arithmetic for backdating commits |
| [`jsonfile`](https://www.npmjs.com/package/jsonfile) | Writing the data scratch file for each commit |
| [`random`](https://www.npmjs.com/package/random) | Generating random week/day positions |
| **Node.js ESM** | Modern ES module syntax (`import`/`export`) |

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

You're free to use, modify, and distribute this for any purpose.

---

<div align="center">

**Made with ❤️ for GitHub profile aesthetics**

If you find this useful, please ⭐ star the repo!

[🐛 Report a Bug](https://github.com/kushdeveloper68/github-graph-art/issues) · [💡 Request a Feature](https://github.com/kushdeveloper68/github-graph-art/issues) · [🔀 Open a PR](https://github.com/kushdeveloper68/github-graph-art/pulls)

</div>