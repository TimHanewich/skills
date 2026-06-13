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
- **One accent, used sparingly.** The accent color is a soft steel blue. It appears on hover states and highlights — not as a background fill for entire sections.
- **Subtle motion over no motion.** Transitions should feel smooth and intentional (0.3s ease), not flashy or distracting.
- **Typography is identity.** The two custom fonts below are non-negotiable for Tim's brand. Do not substitute system fonts or Google Fonts.

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
- [timh-title.woff2](./docs/fonts/timh-title.woff2) for major titles and workmarks.
- [timh-text.woff2](./docs/fonts/timh-text.woff2) for everything else that is intended to be legible and readable.

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

## Individual Elements
There are several formats expected for elements.

### Major Header
For having particularly dramatic text such as a page title, word splash, or wordmark, have it front and center, such as:

```css
h1
{
    font-family: "timh-title";
}
```

```html
<h1 style="text-align: center;">Tim Hanewich Design Principles</h1>
```

## Sub-header
For a sub-header such as a section header of a section of the page, here is an example:

```css
.section-title
{
    border-bottom: solid;
    margin-top: var(--space-medium);
    margin-bottom: var(--space-medium);
    border-bottom: solid;
    border-bottom-width: var(--border-width);
    border-bottom-color: var(--color-separator);
}
```

```html
<h2 class="section-title">Selected Work</h2>
```

### Navigation Header
When placing a header at the very top of a page with multiple options, here is an example:

```css
.header
{
    text-align: center;
    margin-top: var(--space-large);
}

.header a
{
    text-decoration: none;
    margin-left: var(--space-medium);
    margin-right: var(--space-medium);
    margin-top: 0px;
    margin-bottom: 0px;
    display: inline-block;
    transition: margin var(--transition-standard);
}

.header a:hover
{
    color: var(--color-accent);
    margin-left: var(--space-large);
    margin-right: var(--space-large);
}
```

```html
<div class="header">
    <a href="./">Home</a>
    <a href="./">About</a>
    <a href="./">Interest</a>
    <a href="./">Contact</a>
    <a href="./">Meet</a>
</div>
```

### Button
If needing a button, use this:

```css
.button
{
    text-align: center;
    padding: var(--space-small);
    text-decoration: none;
    border-radius: var(--radius);
    border: solid;
    border-width: var(--border-width);
    border-color: var(--color-dark);
    color: var(--color-dark); /* text color */
    transition: background-color var(--transition-standard), color var(--transition-standard), border-color var(--transition-standard);
}

.button:hover
{
    background-color: var(--color-accent);
    color: var(--color-light);
    border-color: var(--color-accent);
}
```

```html
<a class="button" href="./">Example Button</a>
```

### Card
If you would like to have a card that contains information in it, use this:

```css
.card
{
    border: solid;
    border-width: var(--border-width);
    border-color: var(--color-separator);
    border-radius: 8px;
    padding: var(--space-medium);
    background-color: var(--color-light);
    transition: border-color var(--transition-standard);
}

.card:hover
{
    border-color: var(--color-accent);
}
```

And the card would just be a `<div>` that you can also populate with content.

```html
<div class="card">
    <!--some content-->
</div>
```

### Sidebar Navigation
If you'd like to have a sidebar navigation, here is an example of a left-hand one:

```css
.sidebar
{
    width: 220px;
    flex-shrink: 0;
    position: sticky;
    top: 0;
    height: 100vh;
    padding: var(--space-large);
    border-right: solid;
    border-right-width: var(--border-width);
    border-right-color: var(--color-dark);
    display: flex;
    flex-direction: column;
    background-color: var(--color-light);
}

.sidebar .wordmark
{
    font-family: "timh-title";
    font-size: var(--text-medium);
    margin-bottom: var(--space-large);
}

.sidebar a
{
    text-decoration: none;
    padding-top: var(--space-small);
    padding-bottom: var(--space-small);
    padding-left: 0px;
    display: block;
    transition: padding-left var(--transition-standard), color var(--transition-standard);
}

.sidebar a:hover
{
    color: var(--color-accent);
    padding-left: var(--space-small);
}
```

And the HTML example:

```html
<nav class="sidebar">
    <div class="wordmark">Marisol Vega</div>
    <a href="#work">Work</a>
    <a href="#about">About</a>
    <a href="#recognition">Recognition</a>
    <a href="#contact">Contact</a>
</nav>
```

### Activity Log
If needing to have a console-like activity log, you can create one like so to show messages as they appear:

```css
.console
{
    background-color: var(--color-dark);
    border: solid;
    border-width: var(--border-width);
    border-color: var(--color-dark);
    border-radius: var(--border-radius);
    padding: var(--space-medium);
    height: 260px;
    overflow-y: auto;
    font-size: var(--text-small);
    line-height: 1.7;
}

.console .log-line
{
    color: var(--color-light);
    margin: 0px;
    white-space: pre-wrap;
    word-break: break-word;
}

.console .log-time
{
    color: var(--color-accent);
    margin-right: var(--space-small);
}
```

And the HTML:

```html
<div class="console">
    <p class="log-line"><span class="log-time">09:07:39</span>Client comment received on Tideform.</p>
    <p class="log-line"><span class="log-time">09:11:02</span>Generated style tile for Verso Journal.</p>
    <p class="log-line"><span class="log-time">09:14:48</span>Northlight Studio build deployed.</p>
</div>
```

### Text Input
For collecting text input, use the following:

```css
/* Form fields */
.field
{
    margin-bottom: var(--space-medium);
}

.field label
{
    display: block;
    font-size: var(--text-medium);
    margin-bottom: var(--space-small);
}

.input
{
    width: 100%;
    padding: var(--space-small);
    border: solid;
    border-width: var(--border-width);
    border-color: var(--color-muted);
    border-radius: 8px;
    background-color: var(--color-light);
    font-size: var(--text-medium);
    transition: border-color var(--transition-standard);
}

.input:focus
{
    outline: none;
    border-color: var(--color-accent);
}
```

And examples of HTML:

```html
<div class="field">
    <label for="name">Name</label>
    <input class="input" type="text" id="name" name="name" placeholder="Your name">
</div>

<div class="field">
    <label for="email">Email</label>
    <input class="input" type="email" id="email" name="email" placeholder="you@studio.com">
</div>

<div class="field">
    <label for="message">Project details</label>
    <textarea class="input" id="message" name="message" placeholder="Tell me a little about your project..."></textarea>
</div>
```

### Table
For displaying rows of data such as query results or records, wrap the table in a `.table-wrap` (which provides the rounded border and hover accent) and a `.scroll` container so wide tables can scroll horizontally:

```css
.table-wrap
{
    border: solid;
    border-width: var(--border-width);
    border-color: var(--color-separator);
    border-radius: var(--radius);
    overflow: hidden;
    transition: border-color var(--transition-standard);
}

.table-wrap:hover
{
    border-color: var(--color-accent);
}

.scroll
{
    overflow-x: auto;
}

table
{
    border-collapse: collapse;
    width: 100%;
    font-size: var(--text-sm);
}

thead th
{
    text-align: left;
    padding: var(--space-medium);
    border-bottom: solid;
    border-bottom-width: var(--border-width);
    border-bottom-color: var(--color-dark);
    white-space: nowrap;
}

tbody td
{
    padding: var(--space-medium);
    border-bottom: solid;
    border-bottom-width: var(--border-width);
    border-bottom-color: var(--color-separator);
    white-space: nowrap;
}

tbody tr
{
    transition: background-color var(--transition-standard);
}

tbody tr:hover
{
    background-color: #f2f5fb;
}

tbody tr:last-child td
{
    border-bottom: none;
}
```

And the HTML:

```html
<div class="table-wrap">
    <div class="scroll">
        <table>
            <thead>
                <tr>
                    <th>Company</th>
                    <th>Contact</th>
                    <th>City</th>
                    <th>Country</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Alpine Goods</td>
                    <td>Maria Andersen</td>
                    <td>Bergen</td>
                    <td>Norway</td>
                </tr>
                <tr>
                    <td>Harbor Foods</td>
                    <td>Liam O'Brien</td>
                    <td>Cork</td>
                    <td>Ireland</td>
                </tr>
            </tbody>
        </table>
    </div>
</div>
```