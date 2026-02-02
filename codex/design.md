# Watanabe Fishing - Final Design Document

## Design Philosophy

**Core Principle:** This site should feel like it was made by someone who actually fishes Waimanalo, not by a designer who googled "Hawaii fishing."

**The Litmus Test:** If Jay texted this link to his buddies, would they think "oh nice, legit" or "brah why you get one tourist website"?

---

## Anti-Opus Commitments

These are the specific things I will NOT do:

### Layout
- ❌ NO perfectly centered everything
- ❌ NO three-column icon feature cards
- ❌ NO wave SVG section dividers
- ❌ NO gradient overlay on hero with white centered text
- ❌ NO mathematical 80px padding on every section
- ❌ NO "Ready to get started?" generic CTA
- ❌ NO quotation mark graphics on testimonials
- ❌ NO floating/bouncing scroll animations
- ❌ NO parallax

### What I WILL do instead
- ✅ Left-align most text
- ✅ Let the hero image breathe (text small, positioned, not overlaid)
- ✅ Asymmetric layouts with visual tension
- ✅ Vary section rhythm naturally
- ✅ Simple horizontal rules or whitespace between sections
- ✅ Testimonials as plain text with names
- ✅ One specific CTA: "Request Your Session"
- ✅ Static page, hover states only

---

## Color Palette

Hawaii + Japanese subtlety. Not a rainbow. Not teal-coral-purple AI palette.

```
Primary:     #1B4965  (deep ocean blue - like Waimanalo at dusk)
Accent:      #E07A3D  (sunset orange - for CTAs only)
Dark:        #1a1a1a  (near-black for text)
Light:       #f8f7f4  (warm off-white, not pure white - hint of sand)
Muted:       #5a7d8c  (secondary text, faded ocean)
```

**Usage:**
- Background: warm off-white (#f8f7f4)
- Body text: near-black (#1a1a1a)
- Headlines: deep ocean (#1B4965)
- CTA buttons: sunset orange (#E07A3D)
- Links/accents: ocean blue
- One section with inverted dark background (maybe testimonials)

---

## Typography

Two fonts max. Character but readable.

```css
--font-heading: 'DM Serif Display', Georgia, serif;
--font-body: 'DM Sans', system-ui, sans-serif;
```

**Scale (mobile-first):**
```
Hero headline:    clamp(2rem, 8vw, 3.5rem)
Section headers:  clamp(1.5rem, 5vw, 2.25rem)
Body:             1rem (16px base)
Small/meta:       0.875rem
```

**Line heights:**
- Headings: 1.1
- Body: 1.6

**Weight contrast:**
- Headlines: 400 (regular serif reads heavy enough)
- Body: 400
- Emphasis: 600

---

## Layout Structure

### Mobile-first breakpoints
```css
/* Base: 375px mobile */
/* md: 768px tablet */
/* lg: 1024px desktop */
/* max-width: 1200px container */
```

### Spacing system
NOT rigid. Approximate values that breathe:
```
Section padding:  var(--space-section) /* 4rem mobile, 6rem desktop */
Content gap:      var(--space-content) /* 1.5rem - 2rem */
```

---

## Section-by-Section Plan

### 1. Header/Nav (sticky)
```
┌─────────────────────────────────────────────────────────┐
│  WATANABE                    About  Included  Book      │
│  わたなべ                                               │
└─────────────────────────────────────────────────────────┘
```
- Logo: "WATANABE" with small katakana underneath (わたなべ) - Japanese hint
- Right-aligned nav links (no hamburger on desktop, simple hamburger mobile)
- Subtle shadow on scroll
- Height: 60px

### 2. Hero Section
```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  [Full-width hero.png image - already has text baked]   │
│                                                         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```
- hero.png used full-width, aspect-ratio preserved
- NO additional text overlay (image already has title, price, CTA)
- Smooth scroll anchor from the "BOOK NOW" visual to actual form below
- Below hero: small trust line "Shore fishing • Waimanalo, Oahu • Since 2020"

### 3. About Section
```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  LEARN FROM LOCAL                                       │
│                                                         │
│  Watanabe Fishing isn't a tour. No bus, no             │
│  script, no crowd. Just you, the beach, and            │
│  twenty years of Waimanalo shoreline knowledge.        │
│                                                         │
│  Whether you never held a rod or just want to          │
│  fish somewhere new, Watanabe-san will get you         │
│  set up and casting in minutes.                        │
│                                                         │
│  Small groups only. 1-2 people max. Because            │
│  that's how you actually learn.                        │
│                                                         │
│                           [placeholder image: beach]    │
└─────────────────────────────────────────────────────────┘
```
- Left-aligned text
- Single column on mobile, offset two-column on desktop (text left, image right but not 50/50 - more like 60/40)
- Placeholder image slot marked with comment

### 4. What's Included Section
```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  YOUR 4 HOURS                                           │
│                                                         │
│  → All gear provided (rods, tackle, bait)              │
│  → Light refreshments (water, snacks)                  │
│  → Hands-on instruction, start to finish               │
│  → Local knowledge: where, when, what's biting         │
│  → Photos of your catch                                │
│                                                         │
│  $99 per person                                         │
│                                                         │
└─────────────────────────────────────────────────────────┘
```
- Simple list with arrows (→) not icons
- NO card grid
- Price callout prominent but not obnoxious
- Maybe subtle sand/wave texture at bottom (CSS, not SVG wave)

### 5. Testimonials Section (dark background)
```
┌─────────────────────────────────────────────────────────┐
│  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ DARK BACKGROUND ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  │
│                                                         │
│  "Never fished before, now I'm hooked.                 │
│   Watanabe-san made it so easy."                       │
│                                                         │
│   — Kenji M., Honolulu                                 │
│                                                         │
│  ─────────                                             │
│                                                         │
│  "Best morning I've had in years. Caught               │
│   three papio and learned so much."                    │
│                                                         │
│   — Sarah T., visiting from California                 │
│                                                         │
│  ─────────                                             │
│                                                         │
│  "Local knowledge you can't get anywhere else.         │
│   Worth every dollar."                                 │
│                                                         │
│   — Marcus K., Kailua                                  │
│                                                         │
└─────────────────────────────────────────────────────────┘
```
- Dark ocean blue background (#1B4965)
- Light text
- Plain text testimonials, no cards, no quotation graphics
- Simple horizontal lines between
- Stacked vertically (not 3-column grid)

### 6. Book/Contact Section
```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  REQUEST YOUR SESSION                                   │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Name                                             │   │
│  └─────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Email                                            │   │
│  └─────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Phone                                            │   │
│  └─────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Preferred Date                                   │   │
│  └─────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │ How many? [1 ▼] [2]                             │   │
│  └─────────────────────────────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Message (optional)                               │   │
│  │                                                  │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  [ REQUEST INFO ]                                       │
│                                                         │
│  Or call/text: (808) 555-0199                          │
│                                                         │
└─────────────────────────────────────────────────────────┘
```
- Large, touch-friendly inputs
- Simple validation states
- Placeholder submit (form action="#" with success message)
- Phone number below as alternative

### 7. Footer
```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│  WATANABE FISHING                                       │
│  Waimanalo Beach, Oahu                                 │
│                                                         │
│  IG: @watanabefishing (placeholder)                    │
│                                                         │
│  ───────────────────────────────────────────────────   │
│                                                         │
│  © 2025 Watanabe Fishing. All rights reserved.         │
│                                                         │
│  We welcome guests of all abilities. Please contact    │
│  us to discuss any accommodations needed.              │
│                                                         │
│  Come catch choke fish. 🤙                              │
│                                                         │
└─────────────────────────────────────────────────────────┘
```
- Simple, not bloated
- ADA note
- The one "choke fish" moment with shaka
- © 2025

---

## Japanese Design Elements (Subtle)

- Katakana under logo: わたなべ
- Clean negative space (ma - 間)
- Horizontal rules reminiscent of Japanese layouts
- No clutter - restraint is the aesthetic
- Optional: very subtle wave pattern (CSS only) as section texture

---

## Technical Specs

### Performance
- Target: <2s load
- Images: WebP with fallback
- Fonts: Preload DM Serif Display & DM Sans (2 weights max)
- No frameworks, vanilla CSS
- Minimal JS (smooth scroll, form handling, mobile nav toggle)

### Accessibility
- Semantic HTML5 (header, main, nav, section, footer)
- WCAG AA contrast (4.5:1 minimum)
- Focus states visible
- Alt text on all images
- Skip link
- Form labels properly associated

### Mobile
- Touch targets 44x44px minimum
- No horizontal scroll
- Thumb-friendly CTA placement
- Collapsible nav

---

## File Structure

```
/
├── index.html
├── style.css
├── main.js
├── hero.png
└── images/
    └── (placeholder images)
```

No build step needed for production. Vite for dev convenience only.

---

## Final Vibe Check

**Does it feel like:**
- ✅ Jay's buddy made this for him
- ✅ A real local business
- ✅ Simple, confident, trustworthy
- ✅ "I'd actually book this"

**Does it NOT feel like:**
- ❌ A template
- ❌ AI-generated
- ❌ Tourist trap
- ❌ Over-designed
- ❌ Corporate

---

## Sources Referenced

Design trends research:
- [ThunderClap - Best Landing Pages 2026](https://www.thethunderclap.com/blog/best-landing-page-designs)
- [Outbrain - Landing Page Trends 2025](https://www.outbrain.com/blog/landing-page-design-trends/)
- [Framer - Web Design Trends 2025](https://www.framer.com/blog/web-design-trends/)
- [GetResponse - Landing Page Trends](https://www.getresponse.com/blog/landing-page-design-trends)
