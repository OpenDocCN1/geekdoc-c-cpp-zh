# Adding Content Using CSS

For the purposes of search engine optimization and accessibility, it is usually best to keep all content within the `<body>` element of your Web page. If it is dynamically generated, then it will not be seen by web crawlers and many screen readers. However, at times you may have repetitive content that will not help (or even hinder) your placement in a search index.

To add content, you can use the **content** property (Table 9.3), which allows you to specify a text string, image or file URL, quote, or even an attribute value that should be displayed on the page.

# TABLE 9.3 Compatibility

| Value | Compatibility |
| --- | --- |
| normal | IE8, FF1, S1, O4, CSS2 |
| none | IE8, FF1, S1, O4, CSS2 |
| <string> | IE8, FF1, S1, O4, CSS2 |
| <url> | IE8, FF1, S1, O7, CSS2 |
| <counter> | IE8, FF1, S1, O4, CSS2 |
| attr(<selector>) | IE8, FF1, S1, O4, CSS2 |
| open-quote | IE8, FF1, S1, O4, CSS2 |
| close-quote | IE8, FF1, S1, O4, CSS2 |
| no-quote | IE8, FF1, S1, O4, CSS2 |
| no-quote | IE8, FF1, S1, O4, CSS2 |
| inherit |

# To define generated content:

+   1. Specify whether the content should go before or after the element. Type a selector with the `:before` or `:after` pseudo-class (see *Setting the Content Before and After and Element* in Chapter 4) to define where the content will be positioned in relation to the selector (Code 9.3).
2. Add the content property to your CSS. In your declaration block, type the **content** property name, followed by a colon (`:`) and one of the values listed in step 3.

```
.toc h2{...}
```

content:

> Code 9.3 ui-generatedcontent-properties.css—nA flourish image (bullet-01), the word "Chapter" and a counter are inserted before the h2 tag if it is in the .toc class. After bullet is inserted afterward the left

```
*** CSS Q05 | chapter 9 |
-> ui-generatedcontent-properties.css ***

.toc { margin: 0; width: 90%; }
-> text-align: center; font-size: .5em; }

a {
cursor: help; }

h1 {
cursor: url('../images/cursor-02.png');
 20 20, crosshair; }

toc h2:before {
content: url('../images/bullet-01.png');
 'Chapter ' counter(counterNumber) . '.'; }

toc h2:after {
content: url('../images/bullet-02.png'); }
```