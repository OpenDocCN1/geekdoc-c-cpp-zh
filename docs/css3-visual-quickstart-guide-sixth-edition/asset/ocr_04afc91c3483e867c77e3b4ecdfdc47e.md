# # Putting It All Together

Code 6.12 Shows the final results for the file text-properties.css, which we have been building this chapter.

Code 6.12 text-properties.css in its entirety.

```
/*** text-properties.css ***/
body {
    line-height: 1.5; }
h1 {
    letter-spacing: -.05em;
    word-spacing: -1em;
    line-height: .9em;
    text-shadow: 2px 3px 5px rgba(0,0,0,.75); }
h2 {
    letter-spacing: 2px;
    word-spacing: 3px;
    line-height: 1em;
    text-align: center; }
header h2 {
    text-align: right; }
article h2 {
    text-shadow: 0px 1px 1px rgba(255,255,255,.6), 0px -1px 1px rgba(0,0,0,.6); }
h2 .chaptertitle {
    letter-spacing: 0;
    vertical-align: middle; }
p {
    line-height: 2em;
    text-align: justify;
    text-indent: 3em; }
h2 + p {
    text-indent: 0; }
h2 + p:first-letter {
    letter-spacing: -.05em;
    line-height: 24px;
    text-shadow: -3px -3px 3px rgba(153,0,0,.9), 2px 3px 5px rgba(0,0,0,.5); }
address, blockquote {
    text-transform: uppercase;
    white-space: pre; }
a {
    text-decoration: none; }
.delete {
    text-decoration: line-through; }
.pageheader h2 {
    word-spacing: -3em;
    text-align: right; }
.pageheader h2 cite {
    word-spacing: 0;
    text-transform: uppercase;
    vertical-align: -.6em; }
```