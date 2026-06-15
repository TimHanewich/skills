---
name: timh-design
description: "Describes Tim Hanewich's personal UI/UX design taste. This skill overrides default styles to implement Tim's specific taste."
license: MIT
metadata: 
  author: Tim Hanwich
---

# Theme Guide
The following is Tim Hanewich's ("TIMH") personal UI/UX design taste. If you are asked to build a user interface such as a front-end and told to do so with Tim Hanewich's theme in mind, follow these principles.

## Design Philosophy
- **Clean and minimal.** No unnecessary decoration. Every element earns its place.
- **Light by default.** Backgrounds are near-white, not pure white. Text is near-black, not pure black.
- **Accents used sparingly.** The accent color is a soft steel blue. It appears on hover states and highlights, not as a background fill for entire sections.

## Global Preferences
The following design cues should be present across the entire site you make!

### Color Palette
The following is the color palette to use throughout:

```css
:root 
{
    /* Colors */
    --color-light:  #fcfcfc;   /* page background, light surfaces */
    --color-dark:   #1a1a1a;   /* default text, borders, dark surfaces */
    --color-accent: #99B6E8;   /* hover fills, highlights, links */
    --color-muted: #6B6B6B;    /* A dark gray color for captions/footers */
    --color-separator: #E5E5E5 /* A soft, light gray for separators like borders and dividers */
}
```

Note that while above points out suggested uses of these colors, you are welcome to use them whever you feel necessary.

### Fonts
- [timh-title.woff2](./assets/fonts/timh-title.woff2) for major titles and workmarks.
- [timh-text.woff2](./assets/fonts/timh-text.woff2) for everything else that is intended to be legible and readable.

```css
@font-face
{
    font-family: "timh-title";
    src: url("./fonts/timh-title.woff2");
}

@font-face
{
    font-family: "timh-text";
    src: url("./fonts/timh-text.woff2");
}
```

### Font Sizes
Font sizing will use `rem` ("root em"). `16px` will be set as the default with several `rem` variants being used as variables across the entire site.

```css
:root
{
    /* font */
    font-size: 16px;        /* base */
    --text-xl: 3rem;        /* Extra Large, for page titles and other major text */
    --text-lg: 2rem;        /* Large, for section headers and other things */
    --text-md: 1.125rem;    /* Medium, for normal writing */
    --text-sm: 0.875rem;    /* Small, for very small text */
}
```

### Line Heights
Use a standard line-height of 1.2 for everything:
```css
*
{
    line-height: 1.2;
}
```

### Spacing
Use the following spacing variables throughout so spacing is consistent. Never hard-code a raw spacing number unless absolutely necessary.

```css
:root
{
    --space-large:  32px;
    --space-medium: 16px;
    --space-small:  8px;
}
```

### Border Radius
Always use a border radius of `8px` whenever you want a rounded corner:

```css
:root
{
    --radius: 8px;
}
```

### Transitions
For smooth transitions, always encode as 0.3 seconds and `ease`:

```css
:root
{
    --transition-standard: 0.3s ease;
}
```

And then you can use that variable throughout in CSS, as an example:

```css
.header a
{
    transition: margin var(--transition-standard);
}
```

### Border Width
Always use a thin border width of `1px` unless otherwise truly necessary:

```css
:root
{
    --border-width: 1px;
}
```

## Individual Controls
You can use the design language described above to create whatever you want. For common controls, there are also guidelines you can use for each:

| Reference | Description |
| - | - |
| [headers.md](./references/controls/headers.md) | For page titles, wordmarks, and section headers |
| [button.md](./references/controls/button.md) | For interactive buttons |
| [card.md](./references/controls/card.md) | For cards that contain grouped information |
| [console.md](./references/controls/console.md) | For console-like activity logs that show messages as they appear |
| [input.md](./references/controls/input.md) | For collecting text input via form fields |
| [navigation-header.md](./references/controls/navigation-header.md) | For a top-of-page navigation header with multiple options |
| [navigation-sidebar.md](./references/controls/navigation-sidebar.md) | For left-hand sidebar navigation |
| [table.md](./references/controls/table.md) | For displaying rows of data such as query results or records |
| [chat.md](./references/controls/chat.md) | For chat interfaces (e.g. chatbots, messaging) |

If you are asked to build something that requires something *not* in that list (no example implementation), you can invent it yourself using the design styling described above!