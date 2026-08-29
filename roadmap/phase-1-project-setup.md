# Phase 1: Project Setup & Base Styles

> **Estimated Time**: 30–45 minutes  
> **Difficulty**: ⭐ Beginner  
> **Goal**: Set up the project folder structure, create the HTML boilerplate, and establish the foundational CSS styles that the entire project will build upon.

---

## What You Will Build

In this phase, you will create the skeleton of your YouTube Clone project — the folder structure, the HTML document, and the global CSS reset and base styles. By the end, you'll have a blank page that is properly configured and ready for building components.

---

## HTML Concepts Covered

| Concept | Description |
|---|---|
| **HTML5 Boilerplate** | The standard `<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>` structure that every web page starts with. |
| **Meta Tags** | Using `<meta charset="UTF-8">` for character encoding and `<meta name="viewport">` for responsive design. |
| **Linking External Stylesheets** | Connecting CSS files to your HTML using `<link rel="stylesheet">` tags. |
| **Google Fonts Integration** | Using `<link rel="preconnect">` and the Google Fonts API to load custom fonts (Roboto). |
| **Semantic HTML Structure** | Understanding the role of `<header>`, `<main>`, `<nav>`, and `<section>` elements. |

---

## CSS Concepts Covered

| Concept | Description |
|---|---|
| **CSS Reset / Normalization** | Removing default browser styles (margins, paddings) so your layout starts from a clean slate. |
| **`box-sizing: border-box`** | Ensuring padding and borders are included in an element's total width and height — a must-know for predictable layouts. |
| **CSS Custom Properties (Variables)** | Not required at this stage, but a good habit to start defining reusable values like colors and font sizes. |
| **`font-family`** | Setting the base font for the entire page using the imported Google Font. |
| **Universal Selector (`*`)** | Applying styles globally to all elements at once. |

---

## Step-by-Step Instructions

### Step 1: Create the Folder Structure

Create the following folders and files in your project directory:

```
Youtube-Clone/
├── index.html
├── channel-profile/       ← (channel profile images go here)
├── icons/                 ← (SVG icons go here)
│   └── sidebar/           ← (sidebar-specific icons)
├── styles/
│   ├── general.css        ← global reset and base styles
│   ├── header.css         ← (Phase 2)
│   ├── sidebar.css        ← (Phase 3)
│   └── youtube.css        ← main video grid styles (Phase 4)
└── thumbnail/             ← (video thumbnail images go here)
```

> **💡 Tip**: Separating CSS into multiple files by component keeps your code organized and easier to debug. Each file handles one part of the page.

### Step 2: Create the HTML Boilerplate

Open `index.html` and start with the standard HTML5 structure:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Youtube</title>

    <!-- Link your CSS files -->
    <link rel="stylesheet" href="styles/youtube.css">
    <link rel="stylesheet" href="styles/header.css">
    <link rel="stylesheet" href="styles/general.css">
    <link rel="stylesheet" href="styles/sidebar.css">

    <!-- Google Fonts - Roboto -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500;700;900&display=swap"
        rel="stylesheet">
</head>

<body>
    <!-- Components will go here -->
</body>

</html>
```

**Key takeaways:**
- `lang="en"` tells the browser and screen readers the page is in English.
- `viewport` meta tag is essential for mobile responsiveness.
- `rel="preconnect"` tells the browser to establish a connection to Google Fonts early, improving load times.

### Step 3: Write the Global CSS Reset

In `styles/general.css`, add your base styles:

```css
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: "Roboto", Arial, sans-serif;
}
```

**Why this matters:**
- Every browser applies default margins and paddings to elements like `<h1>`, `<p>`, and `<body>`. The `*` selector removes all of them so you have full control.
- `box-sizing: border-box` is arguably the most important CSS rule to learn. Without it, adding padding to a 300px-wide box makes it wider than 300px — which breaks layouts.

### Step 4: Gather Your Assets

Before moving to Phase 2, collect the images and icons you'll need:

- **SVG icons** for the header (YouTube logo, search, hamburger menu, voice search, upload, apps, notifications)
- **SVG icons** for the sidebar (home, explore, subscriptions, originals, YouTube Music, library)
- **Channel profile pictures** (`.jpg` format)
- **Video thumbnails** (`.avif` or `.jpg` format)

> **💡 Tip**: SVG icons are preferred because they scale perfectly at any size without losing quality. You can find free YouTube-style icons on sites like [Heroicons](https://heroicons.com/) or [SVG Repo](https://www.svgrepo.com/).

---

## ✅ Phase 1 Checklist

- [ ] Project folder structure is created
- [ ] `index.html` has a proper HTML5 boilerplate
- [ ] All CSS files are linked in the `<head>`
- [ ] Google Fonts (Roboto) is imported and working
- [ ] `general.css` contains the CSS reset (`margin: 0`, `padding: 0`, `box-sizing: border-box`)
- [ ] Base `font-family` is applied to the `<body>`
- [ ] Asset folders are ready with your icons, thumbnails, and profile images

---

## What's Next?

In [Phase 2: Building the Header](phase-2-header.md), you'll build the YouTube header bar — including the logo, search input, and action icons — using **Flexbox** for layout.
