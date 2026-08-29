# Phase 3: Building the Sidebar

> **Estimated Time**: 30–60 minutes  
> **Difficulty**: ⭐⭐ Beginner–Intermediate  
> **Goal**: Build YouTube's left-side navigation sidebar with vertically stacked icon links using CSS fixed positioning and Flexbox column layout.

---

## What You Will Build

The sidebar is YouTube's primary navigation panel on the left side of the screen. It contains icon links for:

- 🏠 Home
- 🧭 Explore
- 📺 Subscriptions
- 🎬 Originals
- 🎵 YouTube Music
- 📚 Library

Each link consists of an SVG icon stacked above a label, arranged in a vertical column.

---

## HTML Concepts Covered

| Concept | Description |
|---|---|
| **`<nav>` Element** | The semantic HTML5 element used for navigation sections. Screen readers and search engines use this to identify the page's navigation structure. |
| **Icon + Text Pattern** | Pairing an `<img>` icon with a `<div>` text label inside a container — a pattern used across nearly all modern web apps. |
| **Placing `<nav>` Inside `<header>`** | In this project, the sidebar is nested inside the `<header>` tag. While this is a layout choice, understanding where to place navigation elements is an important architectural decision. |

---

## CSS Concepts Covered

| Concept | Description |
|---|---|
| **`position: fixed`** | Pins the sidebar to the left side of the viewport so it stays visible during scrolling — same concept used for the header, but applied vertically. |
| **`top` Offset** | Positioning the sidebar below the header using `top: 56px` (matching the header height) so they don't overlap. |
| **Flexbox Column Layout** | Using `flex-direction: column` to stack sidebar items vertically instead of the default horizontal row. |
| **`align-items: center`** | Centers each icon and label horizontally within the sidebar. |
| **`width` on Fixed Elements** | Setting an explicit width on a fixed-position element since it's removed from the normal document flow. |
| **`font-size` & Spacing** | Controlling text size and margins to match YouTube's compact sidebar typography. |
| **Hover States** | Adding a subtle background color change on hover to indicate interactivity. |
| **`cursor: pointer`** | Signaling to users that sidebar items are clickable. |

---

## Step-by-Step Instructions

### Step 1: Create the Sidebar HTML

Inside your `<header>` element (after the right-section `<div>`), add the sidebar `<nav>`:

```html
<nav class="sidebar">
    <div class="sidebar-link">
        <img src="icons/sidebar/home.svg">
        <div>Home</div>
    </div>
    <div class="sidebar-link">
        <img src="icons/sidebar/explore.svg">
        <div>Explore</div>
    </div>
    <div class="sidebar-link">
        <img src="icons/sidebar/subscriptions.svg">
        <div>Subscriptions</div>
    </div>
    <div class="sidebar-link">
        <img src="icons/sidebar/originals.svg">
        <div>Originals</div>
    </div>
    <div class="sidebar-link">
        <img src="icons/sidebar/youtube-music.svg">
        <div>Youtube Music</div>
    </div>
    <div class="sidebar-link">
        <img src="icons/sidebar/library.svg">
        <div>Library</div>
    </div>
</nav>
```

**Key takeaways:**
- Using `<nav>` tells the browser "this is a navigation region" — important for accessibility and SEO.
- Each `.sidebar-link` follows the same pattern: icon image + text label. Consistency makes your code predictable and easy to maintain.

### Step 2: Style the Sidebar Container

In `styles/sidebar.css`:

```css
.sidebar {
    position: fixed;
    top: 56px;
    left: 0;
    width: 72px;
    height: calc(100vh - 56px);
    background-color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-top: 16px;
    z-index: 50;
}
```

**Why `calc(100vh - 56px)`?**
- `100vh` = the full height of the browser viewport.
- Subtracting `56px` (the header height) ensures the sidebar fills exactly the remaining space below the header.
- `calc()` is a powerful CSS function that lets you mix units — here combining viewport height (`vh`) with pixels (`px`).

**Why `flex-direction: column`?**
By default, Flexbox arranges items in a row (left to right). Setting `column` switches the main axis to vertical, stacking items top to bottom — exactly what we need for a sidebar.

### Step 3: Style Individual Sidebar Links

```css
.sidebar-link {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 72px;
    padding: 16px 0;
    font-size: 10px;
    cursor: pointer;
}

.sidebar-link:hover {
    background-color: #e5e5e5;
}

.sidebar-link img {
    height: 24px;
    margin-bottom: 6px;
}
```

**Layout breakdown:**
- Each link uses `flex-direction: column` to stack the icon above the text.
- `align-items: center` centers both the icon and text horizontally within the link.
- The `10px` font size matches YouTube's compact sidebar typography.
- The `:hover` background change gives users visual feedback that the item is interactive.

### Step 4: Account for Sidebar Width in Main Content

Since the sidebar is `position: fixed`, it's removed from the normal document flow. The main content area doesn't know it exists and will render underneath it. You need to add a left margin to the main content:

```css
/* In youtube.css or general.css */
main {
    margin-top: 56px;    /* Below the fixed header */
    margin-left: 72px;   /* Right of the fixed sidebar */
}
```

> **💡 Important Concept**: Fixed elements are "floating" above the page. Any content behind them will be hidden unless you offset it with margins or padding. This is one of the most common layout bugs beginners encounter.

---

## Understanding Fixed Positioning

Here's a mental model for how the three position types used so far interact:

```
┌──────────────────────────────────────────────┐
│  HEADER (position: fixed, top: 0)            │  ← Always on top (z-index: 100)
├──────┬───────────────────────────────────────┤
│ SIDE │                                       │
│ BAR  │     MAIN CONTENT                      │
│      │     (margin-top: 56px)                │
│ fixed│     (margin-left: 72px)               │
│ top: │                                       │
│ 56px │     This area scrolls normally.       │
│      │     The header and sidebar stay put.  │
│      │                                       │
└──────┴───────────────────────────────────────┘
```

---

## ✅ Phase 3 Checklist

- [ ] `<nav>` element wraps all sidebar links
- [ ] Each link has an SVG icon and a text label
- [ ] Sidebar is fixed to the left side using `position: fixed`
- [ ] Sidebar starts below the header (`top: 56px`)
- [ ] Items are stacked vertically using `flex-direction: column`
- [ ] Icons and labels are centered horizontally
- [ ] Hover effect provides visual feedback
- [ ] Main content area is offset to prevent overlap (`margin-left: 72px`)

---

## What's Next?

In [Phase 4: Building the Video Grid](phase-4-video-grid.md), you'll create the main content area — a responsive grid of video thumbnails with channel info — using **CSS Grid**, the most powerful layout system in CSS.
