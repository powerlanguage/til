I was finding writing markdown on a wide screen frustrating as the lines would in the editor would never wrap.

I think I want different behavior per-language so making a change just for markdown seemed appropriate.

The wrapping has no impact on the contents of the markdown file (soft wrapping instead of hard wrapping).

Add the folowing to your vscode `settings.json`:

```
  "[markdown]": {
    "editor.wordWrap": "wordWrapColumn",
    "editor.wordWrapColumn": 80
  },
```

[source](https://jmarcher.io/vs-code-markdown-and-word-wrap/)
