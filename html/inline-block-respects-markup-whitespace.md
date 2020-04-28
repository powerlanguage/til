`inline` elements respect the whitespace in the markup.

```
.train {
    display: inline-block;
    outline: 1px solid black;
    width: 100px;
    height: 100px;
}

<div class="train"></div>
<div class="train"></div>
<div class="train"></div>
<div class="train"></div>
```

Results in spacing between each element due to the whitespace between each element in the markup (a newline in this case). Removing the spacing in the markup resolves this issue.

```
<div class="train"></div><div class="train"></div><div class="train"></div><div class="train"></div>
```

However, your IDE probably wants to prettify your HTML. If so, you can use CSS to fix the issue.

- `font-size: 0` on parent element
- `display: flex` on parent element

[source](https://stackoverflow.com/questions/19038799/why-is-there-an-unexplainable-gap-between-these-inline-block-div-elements)
