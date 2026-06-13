# Navigation Header
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

