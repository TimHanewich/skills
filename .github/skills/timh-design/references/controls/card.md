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



