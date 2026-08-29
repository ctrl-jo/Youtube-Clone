# Phase 4: Building the Video Grid

> **Estimated Time**: 2–3 hours  
> **Difficulty**: ⭐⭐⭐ Intermediate  
> **Goal**: Build the main content area featuring a responsive grid of video cards — each with a thumbnail, duration badge, channel picture, title, channel name, and metadata — using CSS Grid.

---

## What You Will Build

This is the heart of the YouTube Clone — the video grid that displays video thumbnails in a responsive multi-column layout. Each video card contains:

1. **Thumbnail image** with a time duration overlay
2. **Channel profile picture** (circular avatar)
3. **Video title** (clickable link)
4. **Channel name** (clickable link)
5. **Metadata** (view count and upload date)

---

## HTML Concepts Covered

| Concept | Description |
|---|---|
| **`<main>` Element** | The semantic HTML5 element wrapping the primary content of the page (everything except header, footer, and sidebar). |
| **`<section>` Element** | Groups thematically related content — here, the entire video grid. |
| **`<a>` Anchor Links** | Making thumbnails, titles, and channel names clickable with `href` attributes linking to actual YouTube videos. |
| **`<p>` for Text Content** | Using paragraph elements for video titles, channel names, and view/date metadata. |
| **Nested Link Structures** | Wrapping images and text inside `<a>` tags to create larger clickable areas — a common UI pattern. |
| **HTML Entities** | Using `&#183;` to render the middle dot (·) separator between view count and upload date. |
| **Image Formats** | Understanding the difference between `.avif` (modern, compressed thumbnails) and `.jpg` (widely compatible profile pictures). |

---

## CSS Concepts Covered

| Concept | Description |
|---|---|
| **CSS Grid (`display: grid`)** | The most powerful 2D layout system in CSS. Unlike Flexbox (which is 1D), Grid handles both rows and columns simultaneously. |
| **`grid-template-columns`** | Defines how many columns the grid has and their widths. Using `repeat(4, 1fr)` creates 4 equal-width columns. |
| **`1fr` Unit** | A fractional unit unique to CSS Grid. `1fr` means "one fraction of the available space." Four `1fr` columns split the space equally. |
| **`gap` (Grid Gap)** | Controls the spacing between grid items — both row gap and column gap. |
| **`position: relative` + `position: absolute`** | The parent-child positioning technique used to overlay the time badge on top of the thumbnail image. |
| **`bottom` & `right`** | Positioning the time badge in the bottom-right corner of the thumbnail using absolute positioning offsets. |
| **Sub-Grid with Flexbox** | Inside each video card, using `display: grid` again for the channel picture + info layout (a grid within a grid). |
| **`grid-template-columns: 40px 1fr`** | A two-column sub-grid where the first column is a fixed-width avatar and the second takes the remaining space. |
| **Text Styling** | `font-size`, `font-weight`, `line-height`, `color`, and `text-decoration` for matching YouTube's typography. |
| **`-webkit-line-clamp`** | A CSS property that truncates text after a specified number of lines, adding an ellipsis (...) — used for long video titles. |
| **Link Styling** | Removing default underlines and colors from `<a>` tags with `text-decoration: none` and `color: inherit`. |

---

## Step-by-Step Instructions

### Step 1: Create the Video Grid Container

Inside `<main>` in your `index.html`:

```html
<main>
    <section class="youtube-grid">
        <!-- Video cards go here -->
    </section>
</main>
```

### Step 2: Build a Single Video Card

Each video card follows this structure:

```html
<div>
    <!-- Thumbnail with time badge -->
    <div class="thumbnail-row">
        <a href="https://www.youtube.com/watch?v=VIDEO_ID">
            <img class="thumbnail-img" src="thumbnail/example.avif">
        </a>
        <div class="video-time">6:12</div>
    </div>

    <!-- Video info: channel pic + details -->
    <div class="video-info-grid">
        <div>
            <a href="https://www.youtube.com/@ChannelName">
                <img class="channel-pic" src="channel-profile/example.jpg">
            </a>
        </div>
        <div>
            <a href="https://www.youtube.com/watch?v=VIDEO_ID">
                <p class="video-title">
                    Video Title Goes Here
                </p>
            </a>
            <a href="https://www.youtube.com/@ChannelName">
                <p class="channel-name">
                    Channel Name
                </p>
            </a>
            <p class="video-stats">
                21M views &#183; 11 years ago
            </p>
        </div>
    </div>
</div>
```

**Key takeaways:**
- The thumbnail and time badge are in a `.thumbnail-row` container — this will use `position: relative` so the time badge can be positioned absolutely within it.
- The video info section uses a sub-grid: a fixed-width column for the channel picture and a flexible column for the text.
- All text and images are wrapped in `<a>` tags so users can click through to the actual YouTube content.

### Step 3: Repeat for All Videos

Create 16 video cards (or however many you want) by repeating the pattern from Step 2, updating the thumbnail image, channel picture, title, channel name, and metadata for each.

> **💡 Tip**: While this involves repetitive HTML, it's intentional for a learning project. In a real application, you'd use JavaScript or a framework to dynamically generate these from data.

### Step 4: Style the Grid Layout

In `styles/youtube.css`:

```css
.youtube-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 40px 16px;
    padding: 16px;
}
```

**Understanding `repeat(4, 1fr)`:**
- `repeat(4, ...)` creates 4 columns.
- `1fr` makes each column take an equal fraction of the available width.
- If the container is 1200px wide, each column gets ~300px (minus gaps).

**Understanding `gap: 40px 16px`:**
- First value (`40px`) = row gap (vertical space between rows).
- Second value (`16px`) = column gap (horizontal space between columns).

### Step 5: Style the Thumbnail Row

```css
.thumbnail-row {
    position: relative;
}

.thumbnail-row img {
    width: 100%;
    border-radius: 12px;
}

.video-time {
    position: absolute;
    bottom: 8px;
    right: 8px;
    background-color: rgba(0, 0, 0, 0.8);
    color: white;
    font-size: 12px;
    font-weight: 500;
    padding: 2px 4px;
    border-radius: 3px;
}
```

**The `relative` + `absolute` technique:**
This is one of the most important CSS concepts:

1. The parent (`.thumbnail-row`) gets `position: relative` — this makes it the **positioning anchor**.
2. The child (`.video-time`) gets `position: absolute` — this removes it from the normal flow and positions it **relative to the nearest positioned ancestor**.
3. `bottom: 8px; right: 8px` places the badge 8px from the bottom-right corner of the thumbnail.

```
┌────────────────────────────────┐
│                                │
│        Thumbnail Image         │
│                                │
│                                │
│                        ┌─────┐ │
│                        │6:12 │ │  ← position: absolute
│                        └─────┘ │    bottom: 8px, right: 8px
└────────────────────────────────┘
     position: relative
```

### Step 6: Style the Video Info Section

```css
.video-info-grid {
    display: grid;
    grid-template-columns: 40px 1fr;
    gap: 12px;
    margin-top: 12px;
}

.channel-pic {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    object-fit: cover;
}

.video-title {
    font-size: 14px;
    font-weight: 500;
    line-height: 20px;
    color: #030303;
    margin-bottom: 4px;

    /* Truncate long titles to 2 lines */
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

.channel-name {
    font-size: 12px;
    color: #606060;
}

.video-stats {
    font-size: 12px;
    color: #606060;
}
```

### Step 7: Reset Link Styles

```css
a {
    text-decoration: none;
    color: inherit;
}
```

**Why?** By default, browsers style links with blue text and underlines. `text-decoration: none` removes the underline, and `color: inherit` makes the link use whatever color its parent has — so your carefully chosen text colors aren't overridden.

---

## CSS Grid vs. Flexbox — When to Use Which?

| Scenario | Use |
|---|---|
| Laying out items in a **single row or column** | **Flexbox** (header, sidebar) |
| Laying out items in a **2D grid** (rows AND columns) | **CSS Grid** (video grid) |
| You need items to **wrap to new lines** automatically | **CSS Grid** with `auto-fill` / `auto-fit` |
| You need to **center one item** inside a container | Either works — Flexbox is simpler |
| You need **overlapping elements** | Neither — use `position: absolute` |

In this project:
- **Header** → Flexbox (one row, three sections)
- **Sidebar** → Flexbox with `column` direction (one column, stacked items)
- **Video Grid** → CSS Grid (multiple rows and columns)

---

## ✅ Phase 4 Checklist

- [ ] `<main>` contains a `<section class="youtube-grid">` with all video cards
- [ ] Grid displays 4 columns of equal width using `grid-template-columns: repeat(4, 1fr)`
- [ ] Thumbnails are full-width within their column and have rounded corners
- [ ] Time badge is positioned in the bottom-right corner of each thumbnail
- [ ] Channel pictures are circular (36px × 36px)
- [ ] Video titles are styled with proper font weight and truncated at 2 lines
- [ ] Channel names and metadata use a muted gray color (`#606060`)
- [ ] All links are unstyled (no underline, no blue color)
- [ ] Clicking thumbnails and titles links to actual YouTube videos

---

## What's Next?

In [Phase 5: Responsiveness & Final Polish](phase-5-responsiveness.md), you'll make the entire layout adapt to different screen sizes using **CSS media queries** — the final step to a complete, professional YouTube Clone.
