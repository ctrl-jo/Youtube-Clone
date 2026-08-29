# Phase 2: Building the Header

> **Estimated Time**: 1–2 hours  
> **Difficulty**: ⭐⭐ Beginner–Intermediate  
> **Goal**: Build YouTube's iconic top navigation bar with a logo, search bar, and action icons — all laid out using CSS Flexbox.

---

## What You Will Build

The header is the most recognizable part of YouTube. In this phase, you'll recreate it with three distinct sections:

1. **Left Section** — Hamburger menu icon + YouTube logo
2. **Middle Section** — Search input field + search button + voice search button
3. **Right Section** — Upload, Apps, Notifications icons + profile picture

---

## HTML Concepts Covered

| Concept | Description |
|---|---|
| **`<header>` Element** | The semantic HTML5 element that wraps the top navigation bar of a page. |
| **`<img>` for SVG Icons** | Embedding scalable vector graphics as images for crisp icons at any resolution. |
| **`<input>` Element** | Creating the search text field with `type="text"` and a `placeholder` attribute. |
| **`<button>` Element** | Wrapping icons in buttons for semantic correctness and accessibility. |
| **`<div>` for Grouping** | Using `<div>` containers to group related elements (left-section, mid-section, right-section) for layout purposes. |
| **Nesting Elements** | Building component hierarchies — buttons containing images, divs containing tooltips. |

---

## CSS Concepts Covered

| Concept | Description |
|---|---|
| **Flexbox (`display: flex`)** | The primary layout tool for arranging items in a row. The header is a perfect Flexbox use case — three sections distributed horizontally. |
| **`justify-content`** | Controls horizontal distribution of flex items. Use `space-between` to push the left, middle, and right sections apart. |
| **`align-items: center`** | Vertically centers all items within the header bar. |
| **`position: fixed`** | Pins the header to the top of the viewport so it stays visible while scrolling. |
| **`z-index`** | Ensures the fixed header renders above all other page content. |
| **`padding` & `height`** | Defining the inner spacing and fixed height of the header bar. |
| **Styling `<input>` Fields** | Customizing borders, border-radius, padding, and outline behavior for the search box. |
| **Hover Effects & Tooltips** | Using `:hover` pseudo-class and `opacity`/`visibility` to show tooltips when hovering over icon buttons. |
| **`cursor: pointer`** | Changing the mouse cursor to a pointer hand on interactive elements. |
| **`border-radius`** | Rounding corners on the search button and profile picture (50% for a circle). |
| **`object-fit: cover`** | Ensuring the profile picture fills its container without distortion. |

---

## Step-by-Step Instructions

### Step 1: Create the Header HTML Structure

Inside the `<body>` of your `index.html`, add the header:

```html
<header class="header">
    <!-- Left Section: Menu + Logo -->
    <div class="left-section">
        <img class="hamburger-menu" src="icons/hamburger-menu.svg">
        <img class="youtube-logo" src="icons/youtube-logo.svg">
    </div>

    <!-- Middle Section: Search Bar -->
    <div class="mid-section">
        <input class="yt-textbox" type="text" placeholder="Search">
        <button class="search-button">
            <img class="search-icon" src="icons/search-logo.svg">
            <div class="tooltip">Search</div>
        </button>
        <button class="voice-button">
            <img class="voice-icon" src="icons/voice-search-icon.svg">
            <div class="tooltip">Search with your voice</div>
        </button>
    </div>

    <!-- Right Section: Action Icons + Profile -->
    <div class="right-section">
        <div class="upload-container">
            <img class="upload-icon" src="icons/upload-icon.svg">
            <div class="tooltip">Create</div>
        </div>
        <div class="yt-apps-container">
            <img class="yt-apps-icon" src="icons/youtube-apps-icon.svg">
            <div class="tooltip">Youtube Apps</div>
        </div>
        <div class="notif-icon-container">
            <img class="notifications-icon" src="icons/notifications-icon.svg">
            <div class="tooltip">Notifications</div>
            <div class="notif-count">5</div>
        </div>
        <img class="my-channel-picture" src="channel-profile/channel-profile.jpg">
    </div>
</header>
```

**Key takeaways:**
- The header is divided into three `<div>` sections — this makes Flexbox layout straightforward.
- Each icon button has a nested `<div class="tooltip">` that will appear on hover.
- The notification icon includes a `<div class="notif-count">` badge to display the count.

### Step 2: Style the Header Layout

In `styles/header.css`, start with the overall header:

```css
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    height: 56px;
    padding: 0 16px;
    background-color: white;
    z-index: 100;
}
```

**Why `position: fixed`?**
YouTube's header stays pinned to the top as you scroll. `fixed` takes the element out of the normal document flow and positions it relative to the viewport. The `z-index: 100` ensures it stays above the video grid and sidebar.

### Step 3: Style Each Section

**Left section:**
```css
.left-section {
    display: flex;
    align-items: center;
}

.hamburger-menu {
    height: 24px;
    cursor: pointer;
    margin-right: 16px;
}

.youtube-logo {
    height: 20px;
    cursor: pointer;
}
```

**Middle section (search bar):**
```css
.mid-section {
    display: flex;
    align-items: center;
}

.yt-textbox {
    width: 480px;
    height: 40px;
    padding: 0 12px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 2px 0 0 2px;
    outline: none;
}

.yt-textbox:focus {
    border-color: #1c62b9;
}

.search-button {
    height: 40px;
    width: 64px;
    border: 1px solid #ccc;
    border-left: none;
    background-color: #f8f8f8;
    border-radius: 0 2px 2px 0;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
}
```

> **💡 Tip**: Notice how the search input and button share a border — `border-radius` is set to round only the left side of the input and the right side of the button, creating a seamless joined look.

### Step 4: Add Tooltip Hover Effects

Tooltips are hidden by default and revealed on hover:

```css
.tooltip {
    position: absolute;
    background-color: #606060;
    color: white;
    font-size: 12px;
    padding: 4px 8px;
    border-radius: 2px;
    white-space: nowrap;
    bottom: -36px;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.15s ease-in;
}

.search-button:hover .tooltip,
.voice-button:hover .tooltip,
.upload-container:hover .tooltip,
.yt-apps-container:hover .tooltip,
.notif-icon-container:hover .tooltip {
    opacity: 1;
}
```

**Key learning:**
- `opacity: 0` hides the tooltip while keeping it in the DOM (unlike `display: none`).
- `pointer-events: none` prevents the hidden tooltip from blocking clicks on the button.
- `transition` creates a smooth fade-in animation.
- The `:hover .tooltip` selector means "when hovering over the parent, style the child tooltip."

### Step 5: Style the Profile Picture

```css
.my-channel-picture {
    height: 32px;
    width: 32px;
    border-radius: 50%;
    object-fit: cover;
    cursor: pointer;
    margin-left: 12px;
}
```

**Why `border-radius: 50%`?** This transforms a square image into a perfect circle — the standard look for profile avatars across all social platforms.

**Why `object-fit: cover`?** Without this, a non-square image would be stretched or squished. `cover` ensures the image fills the container while maintaining its aspect ratio, cropping any overflow.

---

## ✅ Phase 2 Checklist

- [ ] Header contains three sections (left, middle, right)
- [ ] YouTube logo and hamburger icon are visible in the left section
- [ ] Search input field and search/voice buttons are styled and aligned
- [ ] Right section icons (upload, apps, notifications) are positioned correctly
- [ ] Profile picture is circular with `border-radius: 50%`
- [ ] Tooltips appear on hover with a smooth transition
- [ ] Notification badge shows a count number
- [ ] Header is fixed to the top of the page using `position: fixed`

---

## What's Next?

In [Phase 3: Building the Sidebar](phase-3-sidebar.md), you'll create the left-side navigation panel with icon links — using **fixed positioning** and **Flexbox column layout**.
