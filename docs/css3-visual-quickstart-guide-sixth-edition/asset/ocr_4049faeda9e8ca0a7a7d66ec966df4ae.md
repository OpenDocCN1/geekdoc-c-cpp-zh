+   5. Link to your *print* style sheet. Immediately after the `<link>` tag, add another `<link>` tag that references the print version of the CSS and define media as print.

```
`<link rel="stylesheet" media="print" href="print.css">`
```

> **TIP** Before media queries were introduced, Web developers used JavaScript to detect browser dimensions and colors. Media queries render those techniques obsolete, at least for styling purposes.

> **TIP** In this example, media queries are applied to the media property value of the `<link>` tag, but you can just as easily apply them to the media property of the `<style>` tag.