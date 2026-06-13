# Table
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