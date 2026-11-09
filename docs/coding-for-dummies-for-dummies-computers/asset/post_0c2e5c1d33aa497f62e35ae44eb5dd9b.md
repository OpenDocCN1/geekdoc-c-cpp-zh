
**Responsiveness:** A fancy word for whether your site will work on mobile phones and tablets in addition to desktop computers. Ordinarily, you would write additional code so your website appears properly on these different screen sizes, but Bootstrap code is already optimized to do this for you, as shown in Figure 8-2.

**Cross-browser compatibility:** Chrome, Firefox, Safari, Internet Explorer, and other browsers all vary in the way they render certain HTML elements and CSS properties. Bootstrap code is optimized so your web page appears consistently no matter the browser used.

![](img/5a907eb39993e80f28c82efc2e4632b3_134_0.png)

*Figure 8-2:* The Angry Birds Star Wars page optimized for desktop, tablet, and mobile using Bootstrap.

## Installing Bootstrap

Install and add Bootstrap to your HTML file by following these two steps:

- 1. **Include this line of code between your opening and closing `<head>` tag:**

    ```html
    <link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    ```

The `<link>` tag refers to version 3.2.0 of the Bootstrap CSS file hosted on the Internet, so you must be connected to the Internet for this method to work.

- 2. **Include both these lines of code immediately before your closing HTML `</body>` tag.**

    ```html
    <!-- jQuery (needed for Bootstrap's JavaScript plugins) -->
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
    <!-- Bootstrap JavaScript plugin file -->
    <script src="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
    ```

![](img/5a907eb39993e80f28c82efc2e4632b3_134_1.png)

The first `<script>` tag references a JavaScript library called jQuery. JavaScript is covered in Chapter 9. Although jQuery is not covered in this book, at a high level, jQuery simplifies tasks performed using JavaScript. The second `<script>` tag references Bootstrap JavaScript plugins, including animated effects such as drop-down menus. If your website does not use any animated effects or Bootstrap JavaScript plugins, you don't need to include this file.

Bootstrap is free to use for personal and commercial purposes, but does require including the Bootstrap license and copyright notice.

If you will not have reliable access to an Internet connection, you can also download and locally host the Bootstrap CSS and JavaScript files. To do this, after unzipping the Bootstrap file, use the `<link>` and `<script>` tags to link to the local version of your file. Visit www.getbootstrap.com/getting-started/ to download the files, and to access additional instructions and examples.

## Understanding the Layout Options

Bootstrap allows you to quickly and easily lay out content on the page using a grid system. You have three options when using this grid system:

- **Code yourself:** After you learn how the grid is organized, you can write code to create any layout you wish.
- **Code with a Bootstrap editor:** Instead of writing code in a text editor, drag and drop components and elements to generate Bootstrap code. You can then download and use this code.
- **Code with a prebuilt theme:** Download free Bootstrap themes or buy a theme where the website has already been created, and you fill in your own content.

### Lining up on the grid system

Bootstrap divides the screen into a grid system of 12 equally-sized columns. These columns follow a few rules:

- **Columns must sum to a width of 12 columns.** You can use one column that is 12 columns wide, 12 columns that are each one column wide, or anything in between.
- **Columns can contain content or spaces.** For example, you could have a 4-column-wide column, a space of 4 columns, and another 4-column-wide column.
- **Unless you specify otherwise, these columns will automatically stack into a single column on smaller browser sizes or screens like mobile devices, and expand horizontally on larger browser sizes or screens like laptop and desktop screens.** See Figure 8-3.

![](img/5a907eb39993e80f28c82efc2e4632b3_136_0.png)

**Figure 8-3:** Sample Bootstrap layouts.

Now that you have a sense for how these layouts appear on the screen, let us take a look at example code used to generate these layouts. To create any layout, follow these steps:

- 1. Create a `<div>` tag with the attribute `class="container"`.
- 2. Inside the first `<div>` tag, create another nested `<div>` tag with the attribute `class="row"`.
- 3. For each row you want to create, create another `<div>` tag with the attribute `class="col-md-X"`. Set X equal to the number of columns you want the row to span.

For example, to have a row span 4 columns, write `<div class="col-md-4">`. The md targets the column width for desktops, and I show you how to target other devices later in this section.

![](img/5a907eb39993e80f28c82efc2e4632b3_136_1.png)

You must include `<div class="container">` at the beginning of your page, and have a closing `</div>` tag or your page will not render properly.

The following code, as shown in Figure 8-4, creates a simple three-column centered layout:

```html
<div class="container">
  <!-- Example row of columns -->
  <div class="row">
    <div class="col-md-4">
      <h2>Heading</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
        tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
        minim veniam, quis nostrud exercitation ullamco laboris nisi ut
        aliquip ex ea commodo consequat
      </p>
    </div>
    <div class="col-md-4">
      <h2>Heading</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      </p>
    </div>
    <div class="col-md-4">
      <h2>Heading</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      </p>
    </div>
  </div>
</div>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_137_0.png)

**Figure 8-4:** Bootstrap three-column layout with desktop (left) and mobile (right) versions.

To see another example, go to the Codecademy site, and resize the browser window. You will notice that as you make the browser window smaller, the columns will automatically stack on top of one another to be readable. Also, the columns are automatically centered. Without Bootstrap, you would need more code to achieve the same effects.

![](img/5a907eb39993e80f28c82efc2e4632b3_137_1.png)

The Lorem ipsum text you see above is commonly used to create filler text. Although the words don’t mean anything, the quotation originates from a first-century BC Latin text by Cicero. You can generate filler text when creating your own websites by using www.lipsum.org or www.socialgoodipsum.com.

### Dragging and dropping to a website

After looking at the code above, you may want an even easier way to generate the code without having to type it yourself. Bootstrap editors allow you to drag and drop components to create a layout, and after which the editor will generate Bootstrap code for your use.

Bootstrap editors you can use include the following:

- **LayoutIt.com:** Free online Bootstrap editor (as shown in Figure 8-5) that allows you to drag and drop components and then download the source code.
- **Jetstrap.com:** Paid online drag and drop Bootstrap editor.
- **Pingendo.com:** Free downloadable drag and drop Bootstrap editor.
- **Bootply.com:** Free online Bootstrap editor with built-in templates to modify.

![](img/5a907eb39993e80f28c82efc2e4632b3_138_0.png)

These sites are free, and may stop working without notice. You can find additional options by using any search engine to search for Bootstrap editors.

![](img/5a907eb39993e80f28c82efc2e4632b3_138_1.png)

**Figure 8-5:** Layoutit.com interface with drag and drop Bootstrap components.

### Using predefined templates

Sites exist that provide ready-to-use Bootstrap themes; all you need to do is add your own content. Of course, you can also modify the theme if you wish. Some of these Bootstrap themes are:

- **Blacktie.co:** Free Bootstrap themes (shown in Figure 8-6), all created by one designer.
- **Bootstrapzero.com:** Collection of free, open-source Bootstrap templates.
- **Bootswatch.com and bootsnipp.com:** Includes pre-built Bootstrap components that you can assemble for your own site.
- **Wrapbootstrap.com:** Bootstrap templates available for purchase.
