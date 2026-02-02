# Design Best Practices

## Layout Principles

### Mobile-First
- Most bookings come from phones
- Design for 375px width first, scale up
- Touch targets minimum 44x44px

### Visual Hierarchy
- One clear CTA per section
- Hero gets the most visual weight
- Testimonials and trust signals support the CTA

### Whitespace
- Generous padding (not cramped)
- Let content breathe
- Sections clearly separated

## Typography

### Font Strategy
- **One font family** (maybe two max)
- System fonts are fine: `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`
- Or a single Google Font like Inter, DM Sans, or Outfit

### Scale
- Base: 16-18px
- Headings: Use a clear scale (1.25 or 1.333 ratio)
- Don't go below 14px for body text

### Line Height
- Body: 1.5-1.6
- Headings: 1.1-1.2

## Color

### Keep It Simple
- One primary color (ocean blue, teal, or similar)
- One accent for CTAs
- Neutral grays for text
- White/off-white backgrounds

### Contrast
- WCAG AA minimum (4.5:1 for text)
- Test with real content

## Images

### Hero Image
- Full-width, high quality
- Jay with the ulua catch
- Consider overlay/gradient for text readability

### Optimization
- WebP format
- Lazy loading for below-fold images
- Proper sizing (not 4000px images scaled down in CSS)

## Components

### Buttons
- Clear hover/active states
- Sufficient padding
- Readable text (not too small)

### Cards (if used)
- Subtle shadows or borders
- Consistent padding
- Don't overdo the styling

### Forms (if contact form)
- Large input fields
- Clear labels
- Obvious submit button

## Performance

- Target < 3s load time
- Minimize JS (vanilla only)
- Compress images
- Use system fonts or limit font weights

## Accessibility

- Semantic HTML (header, main, section, footer)
- Alt text on images
- Keyboard navigable
- Focus states visible
