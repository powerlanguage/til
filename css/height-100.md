`height: 100vh` = 100% of the viewport height
`height: 100%` = 100% of the parent's element height

```
.container {
  display: flex;
  alignItems: center;
  background-color: red;
}


<html>
  <body>
    <div class="container">
      <div>content</div>
    </div>
  <body>
</html>
```

`.container { height: 100vh }` will center vertically.

`.container { height: 100% }` will not, unless you also set `html` and `body` to also have `height: 100%`.

[source](https://stackoverflow.com/questions/27612931/styling-html-and-body-selector-to-height-100-vs-using-100vh)
