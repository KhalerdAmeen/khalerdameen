# PROMPT.md — Claude Code: khalerdameen personal site

## project overview
Build a single-page personal portfolio site for khalerdameen.
Black background. All content center-aligned. Ayuthaya font (Google Fonts).
Fully responsive — centered layout at all screen sizes.
No frameworks. Pure HTML + CSS. One file: index.html.

---

## visual design (from Figma)

### colors
- Background: `#000000`
- Primary text: warm amber/gold — `#C8922A`
- Logo Arabic text: dark green `#2D6A1F` with text-shadow: `3px 3px 0px #8B1A1A, 1px 1px 0px #6B1111`
- Links: `#C8922A`, no underline by default, underline on hover only

### font
- Ayuthaya via Google Fonts
- `<link href="https://fonts.googleapis.com/css2?family=Ayuthaya&display=swap" rel="stylesheet">`
- All text uses Ayuthaya

### layout
- Full viewport black background
- Single centered column: max-width 380px, margin 0 auto
- All text: text-align center
- Padding: 80px 24px
- Gap: logo → tagline ~60px, tagline → projects ~80px, projects → socials ~60px

---

## structure (top to bottom)

### 1. logo
- Arabic text: خالد
- Font size: 100px
- Color: #2D6A1F
- Text shadow: 3px 3px 0px #8B1A1A, 1px 1px 0px #6B1111
- If /public/logo.svg exists, use <img src="/public/logo.svg" height="100" alt="خالد"> instead
- No border, no box

### 2. tagline
22yo founder.
building & scaling brands
- Font size: 13px, color: #C8922A, line-height: 1.8

### 3. projects + credits block
(80px gap below tagline — each item is a plain <a> tag, one per line, no bullets)

<a href="https://khadstudio.co">building Khad Studio</a>
<a href="https://reelhouse.app">building Reelhouse</a>
<a href="https://nextstopai.app/">building Nexstop</a>
<a href="https://routn.lovable.app/">building Routn</a>
<a href="https://www.instagram.com/bykhvlerd/">designed by khalerd.</a>
<a href="https://www.behance.net/khaleedameen">Creative Direction</a>

Font size: 13px, color: #C8922A, line-height: 2, display block

### 4. social block
(60px gap below projects)

Let's connect  ← plain text, not a link
<a href="https://www.instagram.com/bykhvlerd/">ig:@khalerdameen</a>
<a href="https://x.com/khalerdameen">X:@khalerdameen</a>
<a href="https://youtube.com/@khalerddaily">Youtube</a>

Font size: 13px, color: #C8922A, line-height: 2, display block

### 5. footer
© khalerdameen 2026
Font size: 11px, color: #C8922A, opacity: 0.6

---

## link styling
```css
a {
  color: #C8922A;
  text-decoration: none;
  display: block;
}
a:hover {
  text-decoration: underline;
}
a:visited {
  color: #C8922A;
}
```

---

## meta tags
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>khalerdameen</title>
<meta name="description" content="22yo founder. building & scaling brands.">
<meta property="og:title" content="khalerdameen">
<meta property="og:description" content="22yo founder. building & scaling brands.">
<meta property="og:url" content="https://khalerdameen.com">
<meta name="twitter:card" content="summary">
<meta name="twitter:site" content="@khalerdameen">
```

---

## responsiveness
- Black fills 100vw at all widths
- Column stays centered, max-width 380px
- On screens < 380px: padding 16px sides, everything else unchanged
- No horizontal scroll ever

---

## file structure
```
/
├── index.html
├── public/
│   └── logo.svg   (optional — user provides)
├── content.md
└── PROMPT.md
```

---

## rules
- No JS
- No frameworks (no React, no Tailwind)
- All CSS in <style> tag inside index.html
- Valid HTML5
- No additions beyond this spec

---

## after building, ask:
1. "Do you have the logo SVG? Export from Figma → right-click the Arabic خالد text → Copy/Export as SVG → save to /public/logo.svg"
2. "Should I generate a vercel.json?"
3. "Do you want a favicon?"
