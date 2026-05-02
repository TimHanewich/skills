---
name: timh-design
description: Understand Tim Hanewich's personal UI/UX design taste. This skill overrides default styles to implement Tim's specific taste: a high-end, editorial aesthetic defined by Swiss-style typography, monochrome UI foundations, and spacious architectural layouts. Use this to ensure all front-end generation reflects Tim's preference for "photography-first" design and premium performance branding.
license: MIT
metadata: 
  author: Tim Hanwich
---

# Theme Guide
The following is Tim Hanewich's ("TIMH") personal UI/UX design taste. If you are asked to build a user interface such as a front-end and told to do so with Tim Hanewich's theme in mind, follow these principles.

## Theme Summary
This theme is modern, premium, athletic, and editorial. It blends minimalist Swiss-style restraint with bold lifestyle photography. The visual language feels clean, breathable, product-focused, and performance-oriented. It relies heavily on oversized imagery, strong whitespace, crisp typography, and simple black/white foundations with occasional soft neutral or energetic accent colors coming from photography rather than UI chrome.

## Core Brand Feeling
- Premium performance lifestyle
- Minimal, refined, and confident
- Clean and architectural
- High-end retail / direct-to-consumer ecommerce
- Editorial rather than decorative
- Motion, energy, and aspiration

## Visual Principles
1. Let photography do the emotional work.
2. Keep interface chrome minimal and quiet.
3. Use large type with strong hierarchy.
4. Favor spacious layouts with lots of breathing room.
5. Use neutral UI colors so products and images stand out.
6. Avoid ornamental details unless they serve structure or merchandising.

## Color System
### Primary UI Colors
- Background: very light gray to off-white
- Text: deep black or near-black
- Inverse text: white over photography or dark panels
- Borders/dividers: subtle light gray

### Accent Usage
Accents are used sparingly and usually come from product photography rather than interface elements. Typical tones seen in the compositions:
- Soft sky blue
- Muted lavender
- Neon yellow/volt green
- Warm beige/taupe
- Charcoal/graphite
- Golden sunset tones

### Practical Palette Suggestion
- `#F5F5F3` – soft off-white page background
- `#E7E7E4` – card/background gray
- `#D6D6D2` – subtle border/divider
- `#111111` – primary text
- `#000000` – emphasis / dark panels / buttons
- `#FFFFFF` – inverse text
- `#BFD9F6` – optional soft blue accent
- `#D7D1E8` – optional muted lavender accent
- `#C7D600` – optional performance accent

Note: front-end implementation should treat accent colors as secondary to photography. The UI itself should remain mostly monochrome.

## Typography
### Overall Style
Typography is bold, sans-serif, and highly legible. It feels neo-grotesque or Swiss-inspired: clean, direct, modern, and not overly stylized.

### Characteristics
- Large, bold headlines
- Strong contrast between headline and supporting copy
- Tight but readable line spacing on large display text
- Minimal use of italics or decorative type
- Navigation labels are simple and clean
- Category lists use oversized text for emphasis

### Suggested Type Roles
- Hero headline: extra large, bold, clean
- Section headline: large, bold
- Intro/body copy: medium size, regular weight
- Product title: medium, semibold
- Product metadata: small to medium, regular
- Navigation: small to medium, medium weight
- Eyebrow/section label: small uppercase or spaced caps

### Example Type Scale
- Hero display: 56–80px
- Section title: 36–56px
- Card/category title: 24–36px
- Body copy: 18–24px
- Standard UI text: 14–18px
- Meta text: 12–14px

## Layout System
### General Layout Behavior
The layout is modular and spacious. Sections alternate between:
- Full-bleed hero imagery with overlaid text
- Split-screen content blocks
- Three-column editorial/product cards
- Large text lists paired with imagery
- Horizontal product rails
- Mosaic/stacked storytelling panels

### Spacing Philosophy
- Generous outer margins
- Large vertical rhythm between sections
- Comfortable gaps between cards
- Minimal clutter
- Layout breathes more than a typical ecommerce site

### Grid Guidance
- Use a 12-column desktop grid
- Favor asymmetry when it enhances editorial feel
- Let image blocks break strict symmetry occasionally
- Use wide gutters and strong alignment lines
- Mobile should collapse to stacked cards with clear spacing

## Navigation Style
### Header
- Transparent or image-overlay header on hero sections
- White nav/text over dark or photographic hero areas
- Black nav/text on light content backgrounds
- Minimal iconography
- Plenty of horizontal spacing between nav items

### Behavior
- Top navigation is understated and premium
- Menu expansion may reveal a large flyout or split panel
- Secondary links are organized clearly but without heavy containers
- Avoid loud hover effects; keep interactions subtle

## Buttons and Interactive Elements
### Button Style
- Rounded pill buttons
- Solid fills for primary CTA
- Light/white buttons over dark imagery
- Dark/black buttons on light sections
- Secondary buttons remain understated

### Interaction Feel
- Smooth, subtle transitions
- Slight opacity/background shifts on hover
- No flashy gradients or excessive shadows
- Motion should feel premium and restrained

## Card Styles
### Category Cards
- Large photographic cards with minimal bottom-left labels
- Rounded corners are subtle, not overly soft
- Text overlays are simple and high contrast

### Product Cards
- Light neutral product tile background
- Product image centered with ample breathing room
- Wishlist icon small and unobtrusive in top corner
- Product info sits below image, left-aligned
- Badges such as “Bestseller” are small and restrained

### Story/Editorial Cards
- Mix image cards with solid-color quote/statement panels
- Bold white text on dark or photo backgrounds
- Can be used in a horizontal scroll or staggered grid

## Imagery Direction
Photography is the core of the theme.

### Photo Style
- Premium athletic editorial
- Natural motion and candid performance poses
- Full-body or cropped body-detail compositions
- Clean environments with simple backgrounds
- Occasional dramatic lighting or flash photography
- Strong color moments from apparel or outdoor conditions

### Composition Patterns
- Oversized hero crop with subject partially out of frame
- Text anchored in corners over imagery
- Tall portrait cards for categories/storytelling
- Mixed-scale collage layouts
- Product photography on seamless, neutral backgrounds

## Section Patterns to Reuse
### 1. Full-Bleed Hero
- Edge-to-edge image
- Simple top nav overlay
- Large headline bottom-left
- Short supporting sentence
- 1–2 pill CTAs
- Soft gradient or shadow at bottom to preserve text readability

### 2. Split Navigation / Mega Menu
- Left: retained image or page context
- Right: large clean panel with stacked category links
- Primary links are oversized and bold
- Secondary utility links are smaller and placed below

### 3. Three-Up Category Grid
- Three tall cards across desktop
- Each card has large photo and simple corner label
- Light page background with generous gutter spacing

### 4. Activities List + Supporting Image
- Left side: oversized stacked text links
- Right side: one strong editorial image
- High-contrast typography against very light background

### 5. Horizontal Product Carousel
- Large section title above
- Wide product cards on pale gray background
- Minimal product metadata below
- Discreet navigation arrows and progress indicator

### 6. Mission / Brand Story Mosaic
- One large image block
- Several smaller supporting panels overlapping or aligned beside it
- Combination of image panels and dark statement cards
- Large statement heading and short supporting message below

## UI Surface Treatment
- Flat surfaces dominate
- Shadows are minimal to nonexistent
- Contrast comes from scale, photography, and whitespace
- Rounded corners are present but restrained
- Dividers are subtle and sparse

## Motion and Interaction Recommendations
- Use smooth fade/slide transitions
- Keep duration moderate and elegant
- Emphasize content reveal rather than decorative animation
- Product carousels should feel fluid and quiet
- Menus can slide or expand with minimal friction
- Avoid bouncy, playful motion; use refined motion

## Front-End Implementation Guidance
### Best Practices for Developers
- Build the system around reusable content blocks
- Keep a monochrome design token base
- Separate merchandising accents from structural UI styling
- Use image aspect-ratio utilities for consistency
- Design for strong responsive image cropping
- Ensure text overlay contrast is always accessible
- Preserve generous spacing at all breakpoints

### Design Tokens to Define
- Background colors
- Foreground text colors
- Border/subtle divider colors
- Border radius values
- Typography scale
- Spacing scale
- CTA styles
- Overlay gradients for hero readability
- Card aspect ratios

## Recommended Component Library Patterns
- Transparent site header
- Hero banner with overlay content
- Mega menu / flyout navigation
- Image category card
- Product card
- Horizontal product rail
- Editorial split section
- Story mosaic card group
- Primary pill button
- Secondary pill button
- Minimal icon button

## Do
- Use oversized photography
- Use black/white/neutral foundations
- Keep interfaces clean and sparse
- Make typography bold and confident
- Use whitespace as a premium device
- Let merchandising and imagery provide color

## Don't
- Don't overdecorate with gradients, patterns, or heavy shadows
- Don't use too many UI accent colors
- Don't crowd the layout
- Don't use overly playful or whimsical typography
- Don't rely on dense borders or boxed components
- Don't make interactions feel noisy

## Example One-Sentence Theme Prompt
```
Design a premium athletic ecommerce interface with Swiss-inspired minimalism, oversized editorial sports photography, bold sans-serif typography, soft neutral backgrounds, pill-shaped CTAs, spacious modular layouts, and restrained black/white UI styling that lets the products and imagery carry the energy.
```