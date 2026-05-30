# Muskaan Pal — Personal Website

Personal website for Muskaan Pal, a fashion, beauty & lifestyle content creator based in India. The site is a hub for her YouTube/Instagram content and affiliate product recommendations.

**Live:** muskaanpal.in

## Tech Stack

- **Pure static site** — single `index.html` with all CSS and JS inline. No framework, no build step, no dependencies.
- **Fonts:** Google Fonts (Playfair Display for headings, Poppins for body)
- **Icons:** Inline SVGs (YouTube, Instagram, arrows, stars)
- **Embeds:** YouTube iframes (videos + shorts) and Instagram reel iframes

## Project Structure

```
ui/
├── index.html          # Main site (HTML + CSS + JS inline)
├── about.html          # About Me page (detailed bio, original content)
├── privacy-policy.html # Privacy Policy (required for AdSense)
├── terms.html          # Terms of Service
├── ads.txt             # Google AdSense ads.txt
├── logo.png            # Heart-shaped "M" logo (used in nav + favicon)
└── muskaan.JPG         # Hero section portrait photo
```

Everything is in the `ui/` directory. There is no `src/`, no `public/`, no config files.

## Design System

### Colors (CSS custom properties at `:root`)

| Variable      | Value      | Usage                          |
|---------------|------------|--------------------------------|
| `--pink`      | `#e8417a`  | Primary brand color            |
| `--pink-d`    | `#c7305f`  | Hover/active states            |
| `--pink-lt`   | `#fce8f0`  | Light accent backgrounds       |
| `--pink-bg`   | `#fff0f5`  | Section backgrounds            |
| `--dark`      | `#2d0a18`  | Primary text (dark burgundy)   |
| `--gray`      | `#6b7280`  | Secondary/muted text           |
| `--light`     | `#fff5f9`  | Page background                |
| `--white`     | `#ffffff`  | Cards, nav                     |

### Typography

- **Headings:** `'Playfair Display', serif` — weights 700, 900
- **Body:** `'Poppins', sans-serif` — weights 300, 400, 500, 600

### Shared Tokens

- `--radius: 16px` — card border radius
- `--shadow: 0 4px 24px rgba(232,65,122,0.18)` — pink-tinted shadow

## Page Sections (top to bottom)

1. **Nav** — fixed top bar with brand (logo + "Muskaan Pal" text), section links, hamburger menu for mobile. Blur backdrop. Perfumes link has a shimmer animation and "New Picks" tag.
2. **Hero** — two-column (text left, photo right). "Content Creator" badge, heading, description, CTA buttons (YouTube red + Instagram outline), stats row.
3. **Shop / My Picks** — pink background. Affiliate disclosure banner at top. Grid of all product cards (perfume + non-perfume), each with an embedded YouTube short or Instagram reel + affiliate link buttons. Perfume cards appear first, then viral product picks (Bean Bag, Amazon Pinterest Finds, Laneige Lip Mask, Bistro Claytopia, Bath&BodyWorks, Perfume & Mist Stack). Cards support multiple buy links stacked vertically.
4. **Perfumes** — purple-to-pink gradient background. Dedicated fragrance section with 3-column grid of perfume cards. Each card has embedded Instagram reel + multiple affiliate links. Currently has: Armaf Club de Nuit Men / Creed Aventus Dupe (Amazon + Myntra), Maison Asrar Vanilla Voyage (Friday Charm), 5 Must-Have Perfumes (5 Myntra links), Armaf Club De Nuit / Chanel Coco Mademoiselle Dupe (Amazon), Baccarat Rouge 540 dupes — In The Stars, Midnight Bloom, Untold (Amazon), Bath&BodyWorks Covered in Roses / Delina Dupe (Amazon), Perfume & Mist Stack.
5. **Videos** — 2-column grid of embedded YouTube videos with tags and titles.
6. **Social** — two large cards linking to YouTube and Instagram profiles.
7. **Content** — 3-column grid of content category cards (Fashion, Makeup, Lifestyle).
8. **Footer** — dark gradient, brand info, contact email (muskaan5pal@gmail.com), social links, links to Privacy Policy & Terms of Service, copyright.

## Mobile Menu

Hamburger button visible at 768px and below. Opens a dropdown menu with links to all sections. Features:
- Tap feedback: links flash pink for 200ms before menu closes (via `.tapped` class + `setTimeout`)
- Perfumes link is highlighted with shimmer animation + "New Picks" tag
- No hover on mobile (touchscreens) — only tap/active feedback

## Responsive Breakpoints

| Breakpoint | Key changes                                                          |
|------------|----------------------------------------------------------------------|
| `900px`    | Products grid → 2 cols, Perfume grid → 2 cols, Content → 2 cols, Videos → 1 col |
| `768px`    | Nav links hidden, hamburger shown, hero stacks vertically, Perfume grid → 1 col  |
| `480px`    | Product grid 2 cols with tighter gap (12px)                          |

## JavaScript Behavior

- **Auto-scroll on load:** After 300ms delay, scrolls to the Shop section (adjusting for nav height).
- **Smooth scrolling:** Enabled globally via `scroll-behavior: smooth` on `<html>`.
- **Mobile menu:** Toggle open/close via hamburger button. Links close menu with 200ms delay for tap feedback.
- **Shimmer animation:** CSS `@keyframes nav-shimmer` on Perfumes nav link (desktop + mobile).

## External Links & Embeds

- **YouTube channel:** `@muskaan__pal`
- **Instagram:** `@muskaan__pal`
- **Affiliate links:** Amazon (`amzn.to` short links with `rel="sponsored"`), Myntra (`myntr.it`), Friday Charm, Bistro Claytopia
- **Embedded content IDs** are in the iframe `src` attributes in the Shop, Perfumes, and Videos sections.

## Common Changes

### Adding a new product/reel to "My Picks" (Shop)

Add a new `.short-card` inside `.products-grid`:
```html
<div class="short-card">
  <div class="short-embed" style="overflow:hidden;">
    <iframe src="INSTAGRAM_OR_YOUTUBE_EMBED_URL"
      title="TITLE"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen loading="lazy"
      style="margin-top:-54px; height:calc(100% + 54px);">
    </iframe>
  </div>
  <div class="short-info">
    <h4>TITLE</h4>
    <a href="AFFILIATE_LINK" target="_blank" rel="noopener sponsored" class="product-buy" style="text-decoration:none;">Buy on Amazon</a>
  </div>
</div>
```
Note: For YouTube shorts, remove the `style="margin-top:-54px; height:calc(100% + 54px);"` on the iframe (that's only needed for Instagram embeds to hide the IG header).

### Adding a new perfume to the Perfume section

Add a new `.perfume-card` inside `.perfume-grid`:
```html
<div class="perfume-card">
  <div class="perfume-embed" style="overflow:hidden;">
    <iframe src="https://www.instagram.com/p/POST_ID/embed/?hidecaption=true"
      title="TITLE"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen loading="lazy"
      style="margin-top:-54px; height:calc(100% + 54px);">
    </iframe>
  </div>
  <div class="perfume-info">
    <h4>TITLE</h4>
    <div class="perfume-links">
      <a href="LINK" target="_blank" rel="noopener sponsored" class="perfume-link">Buy on Amazon</a>
      <!-- Add more .perfume-link elements for multiple products -->
    </div>
  </div>
</div>
```
Each perfume card supports multiple `.perfume-link` buttons stacked vertically for reels featuring several products.

### Adding a new YouTube video to the Videos section

Add a new `.video-card` inside `.videos-grid`:
```html
<div class="video-card">
  <div class="video-embed">
    <iframe src="https://www.youtube.com/embed/VIDEO_ID"
      title="VIDEO TITLE"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
      allowfullscreen loading="lazy">
    </iframe>
  </div>
  <div class="video-meta">
    <span class="video-tag">TAG</span>
    <h3>VIDEO TITLE</h3>
  </div>
</div>
```

### Changing the hero photo

Replace `ui/muskaan.JPG`. Keep the same filename or update the `<img src>` in the hero section.

### Updating social links

Search for `youtube.com/@muskaan__pal` or `instagram.com/muskaan__pal` — they appear in hero CTAs, social cards, and footer.

## Deployment

Static site — just serve the `ui/` directory. No build step needed. Works with GitHub Pages, Vercel, Netlify, or any static host.

## Notes

- All styles are in a `<style>` tag in `<head>`, not in external CSS files.
- All JS is in a `<script>` tag before `</body>`.
- Image assets are large (logo 1.7MB, hero photo 13MB) — consider compressing if performance matters.
- OG meta tags configured (og:title, og:description, og:image, og:url, twitter:card).
- All video embeds (shorts + reels) use 9:16 aspect ratio via `aspect-ratio: 9 / 16` on `.short-embed` and `.perfume-embed`.
- Affiliate links: Myntra (`myntr.it` short links) for perfumes, Amazon (`amzn.to`) for dupes and other products, Friday Charm for select perfumes.
- **Google AdSense** integrated (`ca-pub-9181267294148574`) with ads.txt, privacy policy, terms of service, and affiliate disclosure for compliance.
- Nav "About" link points to `about.html` (separate page), not an anchor on the main page.
