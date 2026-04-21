# Learn Spanish with Natives — Dev Notes

Static website. No build step, no dependencies. Open `index.html` directly in a browser.

## File structure

```
learnspanishwithnatives.com/
├── index.html          Landing page (hero, how it works, cohorts, testimonials, FAQ, CTA)
├── about.html          Mission, teacher grid (6 cards), teaching approach values
├── pricing.html        3 pricing tiers, comparison table, pricing FAQ
├── contact.html        Contact form (non-functional HTML) + contact details
├── assets/
│   ├── css/
│   │   └── style.css   All styles — single file, section-commented, ~750 lines
│   ├── js/
│   │   └── main.js     Nav scroll, mobile drawer, FAQ accordion, IntersectionObserver fade-ins
│   └── img/
│       ├── logo.png    ← Drop your logo here (referenced as 160×40px in nav)
│       └── favicon.ico ← Drop your favicon here
```

## Adding images

- **Logo**: drop `logo.png` into `assets/img/`. Displayed at `height: 36px` in the nav; aspect ratio is preserved. If the file is missing, the nav falls back to styled text.
- **Hero image**: add `hero.jpg` to `assets/img/`. The hero section will show it at `aspect-ratio: 4/3`, `object-fit: cover`. If missing, a styled cream/gold placeholder shows instead.
- **Teacher photos**: Teacher cards in `about.html` currently use CSS gradient avatars with initials. To add real photos, replace the `.teacher-avatar` div with an `<img>` tag inside `.teacher-card-top`.

## Colours (CSS custom properties)

| Variable       | Hex       | Usage                      |
|---------------|-----------|----------------------------|
| `--maroon`    | `#6B0F0F` | Headings accent, borders   |
| `--gold`      | `#C8930A` | Labels, icons, stars       |
| `--cream`     | `#FAF6EF` | Page background            |
| `--ink`       | `#1A0E0E` | Body text                  |
| `--ink-muted` | `#4A3030` | Secondary text             |
| `--cream-mid` | `#F0E6D8` | Section alternates         |
| `--grad`      | maroon→gold gradient | Buttons, step numbers |

## Typography

Loaded from Google Fonts:
- **Fraunces** (serif, optical sizing) — headings. Weights 300, 400, 600, 700. Italic 400.
- **Inter** (sans) — body. Weights 300, 400, 500, 600.

## Breakpoints

| Name | Width    | What changes                                      |
|------|----------|---------------------------------------------------|
| sm   | 640px+   | 2-col grids (steps, testimonials, teachers, form) |
| md   | 960px+   | Desktop nav, hero 2-col, all 3-col grids          |
| lg   | 1200px+  | Larger section padding                            |

## JavaScript features

All in `assets/js/main.js`, vanilla, no libraries:

- **Nav scroll shadow** — adds `.scrolled` class to `#site-nav` after 8px scroll
- **Mobile drawer** — toggle via `#nav-toggle`, closes on outside click or link click
- **FAQ accordion** — `.faq-item` + `.faq-question` + `.faq-answer` pattern; only one open at a time
- **Fade-in on scroll** — `IntersectionObserver` on `.fade-up` elements; falls back gracefully
- **Smooth scroll** — overrides default anchor scroll to account for sticky nav height
- **Active nav** — sets `.active` on the current page's nav link via `location.pathname`
- **Newsletter form** — prevents submission, swaps placeholder to confirmation message

## Making the contact form functional

The form in `contact.html` is HTML-only. To wire it up:
1. Use a service like [Formspree](https://formspree.io) or [Netlify Forms](https://www.netlify.com/products/forms/)
2. Set `action="https://formspree.io/f/YOUR_ID"` and `method="POST"` on the `<form>` element
3. For Netlify: add `data-netlify="true"` and `name="contact"` attributes

## Deploying

Drop the entire folder on any static host (Netlify, Vercel, GitHub Pages, Cloudflare Pages). No build command needed.
