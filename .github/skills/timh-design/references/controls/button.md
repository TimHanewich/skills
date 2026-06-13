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

