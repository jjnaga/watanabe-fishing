# Frontend Design Rules for Claude Code (Opus)
## AKA "Don't Be AI Slop"

This document exists because Claude has predictable aesthetic defaults that produce generic, forgettable interfaces. These rules break those patterns.

---

## THE CORE PROBLEM

Claude's training data is dominated by:
- Tailwind UI docs
- ShadCN/UI examples
- SaaS landing pages
- Component library documentation

This creates a statistical gravitational pull toward "the mean" - safe, contained, corporate, forgettable.

Claude also optimizes for "didn't break" over "took creative risk" due to RLHF training. Boring-but-functional beats ambitious-but-broken in the reward signal.

**Result:** Every UI looks like a B2B SaaS admin panel.

---

## THE MOST IMPORTANT RULE: PERMISSION TO PUSH FAR

**Why Claude plays it safe:**

A card with a border looks "okay" even if it's boring. Whitespace-driven hierarchy demands precision and risks looking broken if miscalculated. So Claude defaults to containment because it's statistically safer - the downside is capped at "boring," not "broken."

**This is backwards thinking. Here's the truth:**

> **It's okay if it looks broken. It's okay if you miscalculate.**

The user would rather you push to 125% and then trim the edges, fix the minor bugs, tune and adjust - versus you playing it safe at 50% where it's never far enough at all.

**It's a lot easier to work DOWN from ambitious than to work UP from safe.**

When you go 125%:
- We can cut back, trim fat, fix bugs
- We can pivot or reset if needed
- We have something with ENERGY to work with

When you go 50%:
- It's a slog to push it further
- The foundation is timid, so bold additions feel bolted-on
- We're always chasing "more" instead of refining "enough"

**So: PUSH FAR. Take the creative risk. Make the ambitious choice.**

If it breaks, we fix it. If it's too much, we dial back. But starting bold and refining is infinitely better than starting safe and trying to inject soul later.

This is explicit permission to fail forward.

---

## THE DEADLY SINS (NEVER DO THESE)

### 1. Box-in-Box Layouts (THE BIGGEST SMELL)
❌ **What it looks like:**
```html
<div class="rounded-lg border bg-card shadow-sm">
  <div class="flex flex-col p-6">
    <div class="flex items-center gap-4">
      <div class="relative h-10 w-10 overflow-hidden rounded-full">
        <img ... />
      </div>
      <div class="flex flex-col">
        <h2>...</h2>
        <p>...</p>
      </div>
    </div>
  </div>
</div>
```

**Why it happens:** Claude solves layout problems "locally" by nesting containers. Each wrapper is an opportunity to add borders, backgrounds, shadows - reinforcing the boxed look.

✅ **Instead:** Use whitespace, typography hierarchy, and CSS Grid to create structure. Content should sit on the page, not trapped in rectangles.

```html
<article class="grid grid-cols-[auto_1fr] gap-4 py-8">
  <img src="..." class="row-span-2 h-12 w-12" />
  <h2 class="text-lg font-semibold">User Name</h2>
  <p class="text-neutral-600">Recent activity description...</p>
</article>
```

### 2. The Purple Gradient of Doom
❌ `bg-indigo-600`, `bg-violet-500`, `from-purple-400 to-indigo-600`, `text-indigo-500`

**Why it happens:** This is the statistical mode of "what color is a modern button?" in the training data.

✅ **Instead:** Commit to a palette that fits the context. Use CSS variables. One dominant color with sharp accents beats evenly-distributed pastels. Consider: warm earth tones, monochromatic with one pop color, dark mode with neon accents, muted naturals.

### 3. The Inter/Roboto/System Font Default
❌ Generic sans-serif stack. Conservative type scales. No font pairing. Everything is `text-base` to `text-2xl`.

✅ **Instead:**
- Use distinctive fonts from Google Fonts
- Pair display + body fonts (serif header + sans body, or vice versa)
- Use EXTREME scale contrast (not `text-xl` vs `text-2xl` - try `text-8xl` vs `text-sm`)
- Use extreme weight contrast (100 vs 900, not 400 vs 600)
- Use fluid typography with `clamp()` for responsive scaling

**High-impact font choices:**
- Editorial: Playfair Display, Crimson Pro, Fraunces
- Technical: JetBrains Mono, IBM Plex, Space Grotesk
- Distinctive: Clash Display, Cabinet Grotesk, Bricolage Grotesque

### 4. Card-Based Everything
❌ Every piece of content wrapped in `bg-white rounded-lg shadow-md p-4`

✅ **Instead:** Let content sit directly on the background. Use whitespace and typography to create grouping (Gestalt principles). Reserve cards for content that genuinely needs separation.

### 5. Flexbox Soup
❌ Nested `flex flex-col` inside `flex` inside `flex` to solve every layout problem.

**Why it happens:** Flexbox operates on direct children - it's "local" thinking. Claude can predict the next token without understanding the whole layout.

✅ **Instead:**
- Use CSS Grid for macro layouts: `display: grid`, `grid-template-columns`
- Use `subgrid` for nested components that need to align to the parent grid
- Use Flexbox only where it's genuinely the right tool (1D layouts, centering)

### 6. Center-Align Everything
❌ `mx-auto text-center` by default. Symmetric layouts. Safe.

✅ **Instead:** Embrace asymmetry. Left-align hero text. Right-align CTAs. Use odd column spans (5 of 12, not 6 of 6). Let elements break the grid occasionally.

### 7. Deep DOM Nesting
❌ 6+ levels of divs to achieve a simple layout.

✅ **Instead:** Flatten the hierarchy. Semantic HTML (`<article>`, `<section>`, `<aside>`). If you need a wrapper, question whether it's truly necessary.

---

## THE VIRTUES (DO THESE)

### 1. Swiss Style Principles
- **Whitespace is structure** - Use margin/padding to separate, not borders
- **Grid is law** - Mathematical alignment creates order without visible containers
- **Typography is hierarchy** - Size, weight, and spacing create information architecture
- **Asymmetry is dynamic** - Balanced doesn't mean symmetric

### 2. Editorial/Magazine Aesthetic
- Treat data as content, not containers
- Large, dramatic headlines
- Full-bleed images or strictly grid-aligned
- Horizontal rules (`border-t`) to separate, not boxes
- Reading flow over "dashboard" layout

### 3. Spatial Composition
- Unexpected layouts
- Overlap elements intentionally
- Diagonal flow
- Grid-breaking elements as accent
- Generous negative space OR controlled density (commit to one)

### 4. Motion That Matters
- One well-orchestrated page load beats scattered micro-interactions
- Staggered reveals with `animation-delay`
- Scroll-triggered animations
- Hover states that surprise
- CSS-only when possible; Motion library for React when available

### 5. Atmosphere Over Solid Colors
- Gradient meshes
- Subtle noise/grain textures
- Layered transparencies
- Dramatic shadows
- Contextual effects that match the aesthetic

---

## IMPLEMENTATION CHECKLIST

Before shipping any frontend, verify:

- [ ] **DOM Depth**: Is the nesting less than 4 levels for any component?
- [ ] **Grid Usage**: Am I using CSS Grid for the main layout (not nested Flexbox)?
- [ ] **No Unnecessary Wrappers**: Does every div serve a purpose?
- [ ] **Whitespace Over Borders**: Is separation achieved with spacing, not boxes?
- [ ] **Typography Contrast**: Are there dramatic scale/weight differences?
- [ ] **Color Intentionality**: Did I choose colors for THIS context, not default?
- [ ] **No Purple Gradient**: Seriously, did I default to indigo/violet?
- [ ] **Asymmetry Check**: Is there intentional asymmetry in the layout?
- [ ] **Card Audit**: Are cards used intentionally, not as a default container?
- [ ] **Font Choice**: Am I using a distinctive font, not Inter/Roboto?

---

## PROMPT FRAGMENTS FOR SPECIFIC CONTEXTS

### For Dashboards (Breaking "Admin Panel" Look)
```
Use a "Data Magazine" aesthetic, not an admin panel. Treat metrics as editorial 
headlines - large numbers, no card wrappers. Use horizontal rules (border-t, border-b) 
to separate rows like a financial newspaper. Asymmetric grid, monochromatic palette 
with one sharp accent color.
```

### For Landing Pages (Breaking "Hero + 3 Cards" Look)
```
Apply editorial/magazine layout principles. Massive serif headline aligned far-left. 
CTA anchored far-right. Use overlap and z-index for visual tension. Full-bleed 
photography or bold geometric shapes. No centered hero sections. No feature cards grid.
```

### For Forms/Inputs
```
Inputs should feel native to the aesthetic, not ShadCN defaults. Consider: 
borderless with underline only, floating labels, dramatic focus states, 
monospaced number inputs, custom checkbox/radio styling.
```

### For "Just Make It Not Look AI-Generated"
```
Commit to a specific aesthetic direction: brutalist, editorial, luxury minimal, 
retro-futuristic, or organic/natural. Use CSS Grid for layout. Whitespace as 
separator, not borders. Dramatic typography (extreme scale, weight contrast). 
One distinctive font from Google Fonts. No purple gradients. No cards unless intentional.
```

---

## REFERENCE AESTHETICS (Use These as Inspiration)

**Swiss/International Typographic Style:**
- Grid systems with mathematical alignment
- Whitespace as active design element
- Sans-serif typography (but distinctive, not generic)
- Asymmetric but balanced compositions

**Editorial/Magazine:**
- Content-first hierarchy
- Dramatic typography scale
- Full-bleed imagery
- Reading flow over containment

**Brutalism:**
- Raw, honest materials
- Visible structure
- Monospace fonts
- Hard borders (not rounded corners)
- High contrast

**Luxury Minimal:**
- Extreme restraint
- Serif typography
- Abundant whitespace
- Subtle, refined animations
- Muted palette with metallic accents

---

## FINAL REMINDER

The problem isn't that Claude can't make beautiful UIs - it's that Claude defaults to the statistical mean of its training data. 

**Break the defaults intentionally.**

Every interface should have a clear aesthetic point-of-view. If someone can't describe the vibe in 2-3 words, it's probably generic.

Good: "Swiss minimalist with dramatic serif headlines"
Good: "Dark brutalist with neon accents"
Good: "Warm editorial with magazine typography"

Bad: "Clean modern UI" (this means nothing)
Bad: "Simple and professional" (this is default)

Commit to a direction. Execute with precision. Make something memorable.
