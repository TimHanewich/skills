### Console
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
