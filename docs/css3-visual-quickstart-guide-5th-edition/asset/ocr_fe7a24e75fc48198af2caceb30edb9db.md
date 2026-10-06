# Importing style sheet

Another way to bring external style sheets into a document is to use the @import rule. The advantage of importing is that it can be used not only to put an external CSS file in an HTML document file, but also to import one external CSS file into another.

```
rule name
URL for external file
@import url(filename.css);
```

To import an external CSS file:

+   Within the head of your document, add a style element (Code 3.7). This is the same as discussed earlier in this chapter.

<style type="text/css" media="all">...</style>

You can include as many imports as you want, but all of them must be placed before any embedded CSS code in that <style> tag.

+   Add the rest of your embedded CSS. You can include additional embedded CSS rules here, if necessary. (See “Embedded: Adding Styles to a Web Page” this chapter.)

> TIP You can also place @import directly into another external style sheet. This will import the CSS code from one style sheet to the other so that when the second style sheet is linked or imported into an HTML file, the styles from the first style sheet are also included.