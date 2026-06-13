# Major Header
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

