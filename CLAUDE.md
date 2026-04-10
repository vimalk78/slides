# Reveal.js Slide Creation Guide

### Setup
- Single self-contained HTML file per presentation, no local dependencies
- Reveal.js 5.1.0 loaded from CDN: `https://cdn.jsdelivr.net/npm/reveal.js@5.1.0/`
- MathJax 3 from CDN for LaTeX equations
- Dark theme (`black.css`)
- Speaker notes via `<aside class="notes">` (press S to open speaker view)
- Slides repo: `https://github.com/vimalk78/slides` with GitHub Pages enabled
- Each presentation in its own subdirectory (e.g., `tree-pe/`)

### Reveal.js Configuration
- `center: false` does NOT work reliably for top-aligning slides — reveal.js uses `inset: 50%` + `translate(-50%, -50%)` on the `.slides` container, which overrides CSS
- **What works for fitting content**: increase `height` (e.g., 900) and reduce `margin` (e.g., 0.02) instead of fighting the centering
- MathJax renders AFTER reveal.js layout, expanding content and pushing things off-screen. Larger slide height accommodates this
- Recommended config:
  ```js
  width: 1200,
  height: 900,
  margin: 0.02,
  minScale: 0.2,
  maxScale: 1.5,
  center: false
  ```

### Content Preferences
- Left-aligned text (not centered) for content slides
- Title and takeaway slides can be centered (use class `center-slide`)
- Font sizes: h2 at 1.3em, body text at 0.8em, sub-bullets smaller
- Key properties/callouts in a highlighted box (border-left with accent color)
- Use SVG inline for diagrams — not ASCII art (whitespace collapses in divs, and even `<pre>` doesn't look as good)
- Use `<pre>` with `white-space: pre` if ASCII art is needed
- Images from papers: copy to project directory and reference with `<img>` tag; use `background: #fff` and `border-radius: 6px` for paper figures on dark theme

### Math/Equations
- MathJax inline: `\( ... \)`, display: `\[ ... \]`
- Keep display equations in `font-size: 0.85em` or smaller to prevent overflow
- Can color individual matrix entries using `\color{#hex}{value}` inside MathJax
- Equations expand after initial layout — account for this in slide height

### Slide Overflow Prevention
- Do NOT try to CSS-hack reveal.js centering — it fights back
- Instead: increase slide height, reduce font sizes, split content across slides
- Test content-heavy slides with MathJax — they expand after render
- If a slide has text + diagram + equations, it likely needs splitting

### Watermark/Attribution
- Meta tags in `<head>`: author, description, source repo
- Small fixed footer in bottom-left: `position: fixed; bottom: 10px; left: 20px; font-size: 0.65em`
- Link footer to GitHub repo

### Content Approach (from brainstorming)
- Follow the paper's own flow when presenting a paper — it builds intuition in the right order
- Don't dump solutions before motivating them — build up to each reveal
- Use concrete worked examples with actual numbers/matrices
- Speaker notes on every slide for presenter reference
- Keep "explicit hand-holding" sentences out of slides — let examples speak for themselves
- For a study group / blog-style audience: be precise but build intuition incrementally

**Why:** These preferences emerged from extensive iteration on the tree-pe presentation where content overflow, reveal.js centering fights, and MathJax rendering timing caused repeated issues.

**How to apply:** Reference this when creating new presentations in the slides repo. Start with the recommended config, use large slide height, and split content-heavy slides early rather than trying to cram everything in.
