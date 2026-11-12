
## Minify Your CSS

Although creating readable CSS is great for editing and maintaining your code, all of those comments, spaces, and returns end up adding a lot of overhead to your file size. Additionally, although I'm sure you are a fine coder, there is always more room to sort and merge selectors for optimization.

If you want to cut down on your file size, before you deploy your site to the Web, create a minified version of your CSS code. Depending on the size of your CSS file, this can go far to reduce file size.

Don't delete the readable version. You need to keep that version around to make changes.

Minifying your own code is possible but can lead to numerous errors. Fortunately, several online tools are available to help you. My favorite is Minify CSS's CSS Compressor & Minifier A.

![](img/e1ed1e3c1873fa9fc855210fb83699d0_417_0.png)

The Minify CSS Compressor page at www.minifycss.com/css-compressor.

### Code 15.5 My CSS code before being minified.

```
/* *** box-properties.css *** */
body {
 margin: 0;
 padding: 0;
}
header, section, nav, article, aside, figure,
 figcaption, footer, hgroup {
 display: block; }
header, footer {
 clear: both;
 width: 100%; }
header {
 height: 135px; }
footer {
 height: 40px;
 padding: 30px 0 10px 0;
 text-align: center; }
h1 {
 width: 95%;
 max-width: 980px;
 min-width: 660px;
 margin: 0 20px 10px 5%;
 padding-top: 10px; }
hgroup h2 {
 margin: 30px;
 width: 95%; }
article h2 {
 width: 95%;
 margin-bottom: 60px; }
article {
 width: 80%;
 max-width: 980px;
 min-width: 660px;
 margin: 150px 0 10px 0;
 border-top-right-radius: 20px;
 border-top: 10px transparent solid;
 border-right: 10px transparent solid;
 padding: 80px; }
article p {
 margin: 0; }
article h2 + p {
 margin-bottom: 1em;
 padding-bottom: 1em;
 -webkit-column-count: 2;
 -moz-column-count: 2;
 column-count: 2;
 -webkit-column-gap: 4em;
 -moz-column-gap: 4em;
 column-gap: 4em;
 -webkit-column-rule: 2px groove
 rgba(0,0,0,.5);
 -moz-column-rule: 2px groove rgba(0,0,0,.5);
 column-rule: 2px groove rgba(0,0,0,.5); }
article h2 + p:first-letter {
 float: left;
 display: block;
 margin: -3.5em .2em .2em 0;
 padding: 0; }
aside {
 width: 200px;
 height: 400px;
 overflow: auto;
 border-radius: 20px/40px;
 padding: 20px; }
footer nav a {
 margin: 0 1em; }
footer nav a:hover {
 outline: rgba(135,127,107,.65) 10px double; }
figure {
 border: 6px double rgba(142, 137, 129,.5);
 clear: both; }
figure img {
 margin: 0; }
figure.c-illo {
 border-radius: 10px; }
figure.bw-illo {
 border: 1em double rgba(142, 137, 129,.5);
 -webkit-border-image: url(../images/chrome/
 border-02.png) 27 round;
 -moz-border-image: url(../images/chrome/
 border-02.png) 27 round;
 -o-border-image: url(../images/chrome/
 border-02.png) 27 round;
 border-image: url(../images/chrome/
 border-02.png) 27 round; }
figcaption {
 border-top: 2px solid rgba(142, 137, 129,.5);
 padding: 10px; }
.floatleft {
 float: left;
 margin: 1em 2em 1em 0; }
.floatright {
 float: right;
 margin: 1em 0 1em 2em; }
.floatcenter {
 margin: 1em auto; }
```

## To minify your CSS:

- 1. Visit Minify CSS. Once you have finished your CSS code and are ready to go live on the Web, point your browser to www.minifycss.com/css-compressor.

- 2. Load your CSS code. You can either paste it directly into the form field or enter a URL from which to grab the CSS (Code 15.5). I pulled this code from Chapter 10.

- 3. Choose your options. Experiment to get the desired effect, but remember that your goal is to reduce your code file size as much as possible. You can also choose whether to output the CSS code for you to copy or as a separate CSS file.

```
-moz-column-rule: 2px groove rgba(0,0,0,.5);
column-rule: 2px groove rgba(0,0,0,.5); }
article h2 + p:first-letter {
float: left;
display: block;
margin: -3.5em .2em .2em 0;
padding: 0; }
aside {
width: 200px;
height: 400px;
overflow: auto;
border-radius: 20px/40px;
padding: 20px; }
footer nav a {
margin: 0 1em; }
footer nav a:hover {
outline: rgba(135,127,107,.65) 10px double; }
figure {
border: 6px double rgba(142, 137, 129,.5);
clear: both; }
figure img {
margin: 0; }
figure.c-illo {
border-radius: 10px; }
figure.bw-illo {
border: 1em double rgba(142, 137, 129,.5);
-webkit-border-image: url(../images/chrome/
border-02.png) 27 round;
-moz-border-image: url(../images/chrome/
border-02.png) 27 round;
-o-border-image: url(../images/chrome/
border-02.png) 27 round;
border-image: url(../images/chrome/
border-02.png) 27 round; }
figcaption {
border-top: 2px solid rgba(142, 137, 129,.5);
padding: 10px; }
.floatleft {
float: left;
margin: 1em 2em 1em 0; }
.floatright {
float: right;
margin: 1em 0 1em 2em; }
.floatcenter {
margin: 1em auto; }
```

- 4. Process CSS. Click the Process CSS button under the field where you added your code. After a few seconds, a list of messages will appear showing the invalid properties discovered. Under that is your code to download or copy (Code 15.6).

- 5. TEST, TEST, TEST! Depending on how much you compressed your code, it may have changed a little or a lot. Regardless, it's different and may behave differently. If you encounter problems with the new CSS code, try minifying it again using different settings.

### Code 15.6 The same CSS code after being minified.

```
body{margin:0;padding:0;}header,section,nav,article,aside,figure,figcaption,footer,hgroup{display:block;}header,footer{clear:both;width:100%;}header{height:135px;}footer{height:40px;padding:30px 0 10px;text-align:center;}h1{margin:0 20px 10px 5%;max-width:980px;min-width:660px;padding-top:10px;width:95%;}hgroup{margin:0;}article h2{margin-bottom:60px;width:95%;}article{border-right:10px transparent solid;border-top:10px transparent solid;border-top-right-radius:20px;margin:150px 0 10px;max-width:980px;min-width:660px;padding:80px;width:80%;}article h2 + p{-moz-column-count:2;-moz-column-gap:4em;-moz-column-rule:2px groove rgba(0,0,0,.5);-webkit-column-count:2;-webkit-column-gap:4em;-webkit-column-rule:2px groove rgba(0,0,0,.5);column-count:2;column-gap:4em;column-rule:2px groove rgba(0,0,0,.5);margin-bottom:1em;padding-bottom:1em;}article h2 + p:first-letter{display:block;float:left;margin:-3.5em .2em .2em 0;padding:0;}aside{border-radius:20px/40px;height:400px;overflow:auto;padding:20px;width:200px;}footer nav a{margin:0 1em;}footer nav a:hover{outline:rgba(135,127,107,.65) 10px double;}figure{border:6px double rgba(142,137,129,.5);clear:both;}figure img{margin:0;}figure.c-illo{border-radius:10px;}figure.bw-illo{border:1em double rgba(142,137,129,.5);-webkit-border-image:url(../images/chrome/border-02.png) 27 round;-moz-border-image:url(../images/chrome/border-02.png) 27 round;-o-border-image:url(../images/chrome/border-02.png) 27 round;border-image:url(../images/chrome/border-02.png) 27 round;}figcaption{border-top:2px solid rgba(142,137,129,.5);padding:10px;}.floatleft{float:left;margin:1em 2em 1em 0;}.floatright{float:right;margin:1em 0 1em 2em;}.floatcenter{margin:1em auto;}article p,figure img{margin:0;}
```

## 33 CSS Best Practices

Throughout the pages of this book, I’ve offered numerous tips, recommendations, and suggestions. I’ve tried to follow my own advice in all of the code I’m presenting, but the necessities of creating useful examples had to be balanced against the needs of best practices for coding. So, to clear up any confusion, here are the 33 most important best practices for CSS, along with cross-references showing where you can find additional information.

- 1. Always specify units for values except when the value is 0. It’s a simple equation:

```
0px = 0in = 0em = 0cm = 0% = 0mm = 0
```

Zero is always zero, and you don’t need to define what kind of 0 it is.

See “Values and Units Used in This Book” in the Introduction.

- 2. Structure first, then presentation. Some designers want to start designing pages without first placing the HTML structure, but this is like trying to put siding on a house that hasn’t been framed yet.

See “How Does HTML5 Structure Work?” in Chapter 2.

- 3. Specify a doctype. These days, using a DTD should go without saying, but an HTML document without a doctype is like a book without a cover. Not only do you not know what’s in it, but the whole thing tends to fall apart.

See “How Does HTML5 Structure Work?” in Chapter 2.

- **4. All styles should be external.** To keep the Web site as easy to change as possible, the final styles should always be located in external files and never be embedded in the head or inline. Embedded or inline styles are acceptable during development but should all be moved into an external style sheet before deployment.

See “External: Adding Styles to a Web Site” in Chapter 3.

- **5. Keep the number of external style sheets to a minimum.** This may seem to contradict the previous statement, but every external style sheet is a call to the Web server, and every call slows down Web page loading. This is true whether you are using <link> or @import.

See “External: Adding Styles to a Web Site” in Chapter 3.

- **6. Place style links in the <head>, never in the <body>.** Styles placed in the <body> of an HTML document will not be applied to the page until after the Web page has displayed, causing the entire document to briefly flash as it re-renders the page with the styles. This is annoying and unattractive.

See “External: Adding Styles to a Web Site” in Chapter 3.

- **7. Use link to add styles to an HTML document and @import to add styles to other style sheets.** Older versions of Internet Explorer will load styles in the <head> as if they were in the <body>, causing the annoying flash as the page re-renders.

See “External: Adding Styles to a Web Site” in Chapter 3.
