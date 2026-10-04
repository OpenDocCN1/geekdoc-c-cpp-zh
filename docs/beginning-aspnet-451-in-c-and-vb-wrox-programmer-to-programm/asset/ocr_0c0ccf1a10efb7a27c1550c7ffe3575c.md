To summarize, formatting with HTML suffers from the following problems:

+   - Its feature severely limits the formatting possibilities that your pages require.

+   - Data and presentation are mixed within the same file.

+   - HTML does not enable you to easily change formatting at run time in the browser.

+   - The required formatting tags and attributes make your pages larger and slower to load, display, and maintain.

Fortunately, CSS enables you to overcome all of these problems.

# # How CSS Fixes Formatting Problems

CSS is designed to format your web pages in almost every possible way. It offers a rich set of options to change every little aspect of your page, including fonts (size, color, family, and so), and background colors, borders around HTML elements, positioning of elements in your page, and much more. CSS is understood by all major browsers today, so it's the language for visual presentation of web pages and very popular among web developers.

CSS overcomes the problem of mixed data and presentation by enabling you to define all formatting in external files. Your ASPX or HTML pages reference these files and the browser will apply the styles you prefer. With this, the HTML document contains what you want to display, and the CSS defines how you want to display, enabling you to change or replace one of the documents, leaving the other unmodified. In addition, you can place CSS directly in an HTML or ASPX page, which gives you a chance to add small snippets to CSS exactly where you need them. You should be cautious when placing CSS directly in an HTML or ASPX page, because you can no longer control style information from a single, central location.

Because you place all CSS in a separate file, it's easier to offer the choice between different styles—for example, one with a larger font size. You can create a copy of the external style sheet, make the necessary changes, and then offer this alternative style to the user. You can see how this works in Chapter 6 when ASP.NET Themes are discussed.

Another benefit of a separate style file is the decreased bandwidth which is required for your site. Style sheets don't change with each request, so a browser saves a local copy of the style sheet the first time it downloads it. Then on,, it uses this cached copy of requesting it from the server over and again. Sometimes this caching can work when the browser doesn't download. If you find that the browser is not picking up the changes you made to a CSS file, use Ctrl+F5 or Ctrl+R in the browser (not in VS) to get a fresh copy from the server.

Now that you have seen why CSS is so important, it is time to find how it works and how to use it.

# # INTRODUCTION TO CSS

In terms of syntax, CSS is an easy language to learn. Its “grammar” consists of only a few concepts. That makes it relatively easy to get started with. What makes CSS a bit more difficult is the way all major browsers render a page. Although virtually every modern desktop browser understands CSS, they all have their quirks when it comes to displaying a page according to the CSS standard.