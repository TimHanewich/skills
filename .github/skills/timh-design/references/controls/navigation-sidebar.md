# Navigation Sidebar
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

