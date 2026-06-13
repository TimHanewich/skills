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
