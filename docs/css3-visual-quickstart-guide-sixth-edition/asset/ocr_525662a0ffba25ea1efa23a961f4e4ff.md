Code 14.8 small.css contains all of the default styles used in the site plus layout styles for smaller screens. To save space, I’ve added the styles from Chapters 5–10 using @import to bring those other files into this one, but generally this technique is not recommended (see Chapter 3 for details).

```
/*** small.css - Default Styles ***/

@import url("../css/font-properties.css");
@import url("../css/text-properties.css");
@import url("../css/color-background-properties.css");
@import url("../css/list-table-properties.css");
@import url("../css/ui-generatedcontent-properties.css");

h1 {
    font-size: 3em; }

p {
    width: 94%; }

nav.toc {
    color: rgba(255,255,255,.75);
    margin: 0;
    padding: 0;
    width: 93%; }

nav.toc ol, nav.toc ul, nav.toc li {
    background: rgba(0,0,.5);
    border-bottom: 1px solid rgb(153,153,153);
    list-style: none;
    margin: 0 0 -4%;
    padding: .5em 5%;
    width: 100%; }

aside {
    padding: 5%;
    width: 91%; }
```

Code 14.9 medium.css provides adaptive styles for medium-size devices, which in this case means changing the header size.

```
/*** Medium Device Styles ***/

h1 { font-size: 4em; }
```