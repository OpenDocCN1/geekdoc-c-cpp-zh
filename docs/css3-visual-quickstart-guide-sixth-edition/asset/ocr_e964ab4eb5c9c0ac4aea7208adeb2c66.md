# # Minify Your CSS

Although creating readable CSS is great for editing and maintaining your code, all of those comments, spaces, and returns end up adding a lot of overhead to your file size. Additionally, although I'm sure you are a fine coder, there is always more room to sort and merge selectors for optimization.

If you want to cut down on your file size, before you deploy your site to the Web, create a minified version of your CSS code. Depending on the size of your CSS file, this can go far to reduce file size.

Don't delete the readable version. You need to keep that version around to make changes.

Minifying your own code is possible but can lead to numerous errors. Fortunately, several online tools are available to help you. My favorite is Minify CSS's CSS Compressor & Minifier A.

![](bbox=[0.09, 0.53, 0.49, 0.83])

The Minify CSS Compressor page at www.minifycss.com/css-compressor.

# ### Code 15.5 My CSS code before being minified.

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
 margin-bottom: 60px; } article {
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
 -webkit-kit-column-rule: 2px groove
 rgba(0,0,0,.5); }
```