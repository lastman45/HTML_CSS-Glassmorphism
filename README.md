# GlassMorphism Login Page

A stylised login form built with pure HTML and CSS, featuring the **glassmorphism** design trend — frosted-glass UI cards layered over animated gradient backgrounds.

---

## Table of Contents

- [Overview](#overview)
- [Project Structure](#project-structure)
- [Features](#features)
- [Known Bugs & Fixes](#known-bugs--fixes)
- [Usage](#usage)
- [Customisation](#customisation)
- [Browser Compatibility](#browser-compatibility)
- [Dependencies](#dependencies)

---

## Overview

Glassmorphism is a UI design language characterised by:

- **Translucent surfaces** — `background: rgba(255,255,255,0.1)`
- **Blur effects** — `backdrop-filter: blur(15px)`
- **Subtle borders** — `border: 1px solid rgba(255,255,255,0.4)`
- **Layered depth** — cards that appear to float above a vivid background

This project implements those principles in a simple, self-contained login form with animated label transitions, a shimmer hover effect on the card, and a live animated gradient background.

---

## Project Structure

```
GlassMorphism/
├── GlassMorphism.html   # Markup — login form and page structure
└── GlassMorphism.css    # Styles — glassmorphism effects, layout, animations
```

The HTML file links to the CSS file via a relative `<link>` tag, so both files must be kept in the **same directory**.

---

## Features

### Animated Gradient Background
The `body` uses a `linear-gradient` with `background-size: 400% 400%` and the `gradientBG` keyframe animation to create a slow, looping colour-shift effect across four colours.

```css
animation: gradientBG 14s ease infinite;
```

### Frosted Glass Card
The `.glass-container` is the centrepiece — it uses:

| Property | Value | Effect |
|---|---|---|
| `backdrop-filter: blur(15px)` | Blurs everything behind the card | Frosted glass look |
| `background: rgba(255,255,255,0.1)` | 10% white fill | Translucency |
| `border: 1px solid rgba(255,255,255,0.4)` | Semi-transparent border | Glass edge highlight |
| `box-shadow: 0 25px 45px rgba(0,0,0,0.4)` | Deep shadow | Floating depth |

### Shimmer Hover Effect
A `::before` pseudo-element sweeps across the card on hover, simulating a light reflection. It starts at `left: -100%` and transitions to `left: 120%` on `:hover`.

### Floating Labels
Input labels are positioned absolutely over the input field. When the input is focused or has a value (`:valid`), the label animates upward and shrinks — creating a clean "floating label" UX pattern with no JavaScript required.

```css
.input-group input:focus + label,
.input-group input:valid + label {
    top: 0;
    font-size: 12px;
}
```

> **Note:** This relies on the `required` attribute being set on inputs. Without `required`, `:valid` matches even when the field is empty, and the label floats permanently.

### Login Button
The `.login-btn` lifts on hover via `transform: translateY(-3px)` and brightens its background, giving satisfying tactile feedback.

---

## Known Bugs & Fixes

The original source files contain **6 bugs** that prevent the page from rendering correctly. The table below documents each one.

| # | File | Location | Bug | Fix |
|---|------|----------|-----|-----|
| 1 | `GlassMorphism.css` | `.glass-container` | `height: 40px` collapses the card to a thin sliver, hiding all form content | Replace with `padding: 40px 35px 35px` so the card sizes to its content |
| 2 | `GlassMorphism.css` | `body` | `background: url()` — empty `url()` produces no background; the animated gradient has nothing to display | Replace with a real `linear-gradient(-45deg, ...)` with `background-size: 400% 400%` |
| 3 | `GlassMorphism.css` | `.glass-container::before` | `transform: 0.5s` is not a valid CSS declaration — the shimmer sweep animation is broken | Change to `transition: 0.5s` |
| 4 | `GlassMorphism.css` | `.remember-forgot` | `justify-content: center` with no `gap` causes "Remember me" and "Forgot Password?" to overlap each other | Change to `justify-content: space-between` |
| 5 | `GlassMorphism.html` | `.register-link` div | `<div class="register-link">` is never closed — the `</div>` before `</form>` is missing, producing invalid HTML | Add `</div>` after the `<p>` tag |
| 6 | `GlassMorphism.html` | Font Awesome `<link>` | `font-awesome/7.0.0` does not exist on cdnjs — icons silently fail to load | Update to `font-awesome/6.5.0` (latest stable release) |

---

## Usage

### Running Locally

No build tools or server required. Open the HTML file directly in a browser:

```bash
# macOS
open GlassMorphism.html

# Windows
start GlassMorphism.html

# Linux
xdg-open GlassMorphism.html
```

Both files must be in the same folder because `GlassMorphism.html` references `GlassMorphism.css` with a relative path:

```html
<link rel="stylesheet" href="GlassMorphism.css">
```

### Embedding in a Project

Copy both files into your project directory. If you rename or move the CSS file, update the `href` in the `<link>` tag accordingly.

---

## Customisation

### Changing the Background Gradient

Edit the four colours in the `body` background property in `GlassMorphism.css`:

```css
body {
    background: linear-gradient(-45deg, #1a1a2e, #16213e, #0f3460, #533483);
}
```

Change the hex values to any colours you like. The `gradientBG` animation will automatically cycle between them.

### Adjusting the Animation Speed

The gradient animation duration is controlled by `14s` in:

```css
animation: gradientBG 14s ease infinite;
```

Lower the value for a faster cycle, raise it for a slower one.

### Card Width

The card width is set on `.glass-container`:

```css
width: 380px;
```

Change this to adapt the form for different screen sizes. For a responsive layout, replace with a percentage and add a `max-width`:

```css
width: 90%;
max-width: 420px;
```

### Glass Opacity

Adjust the translucency of the card by changing the alpha value in `rgba(255, 255, 255, 0.1)`:

```css
background: rgba(255, 255, 255, 0.1); /* 0.0 = invisible → 1.0 = solid white */
```

Increase it toward `0.2`–`0.3` for a more opaque card; reduce it toward `0.05` for a more transparent one. Pair with the `blur` value for best results.

### Blur Intensity

The blur strength is on `.glass-container`:

```css
backdrop-filter: blur(15px);
-webkit-backdrop-filter: blur(15px); /* Add for Safari support */
```

Values between `8px` and `20px` work best for readability.

---

## Browser Compatibility

| Feature | Chrome | Firefox | Safari | Edge |
|---|---|---|---|---|
| `backdrop-filter` | ✅ 76+ | ✅ 103+ | ✅ 9+ (with `-webkit-`) | ✅ 79+ |
| CSS custom animations | ✅ | ✅ | ✅ | ✅ |
| `:focus` / `:valid` selectors | ✅ | ✅ | ✅ | ✅ |
| `accent-color` | ✅ 93+ | ✅ 92+ | ✅ 15.4+ | ✅ 93+ |

> **Safari note:** Add `-webkit-backdrop-filter: blur(15px)` alongside `backdrop-filter` for full Safari support.

---

## Dependencies

| Dependency | Version | Purpose | CDN |
|---|---|---|---|
| Font Awesome | 6.5.0 | Icon library (if icons are added to inputs or buttons) | `cdnjs.cloudflare.com` |

Font Awesome is linked in the HTML but no icons are currently used in the markup. The link can be removed if icons are not needed, which will slightly improve load time.

---

## License

This project is provided for educational and personal use. No license is attached — adapt freely.
