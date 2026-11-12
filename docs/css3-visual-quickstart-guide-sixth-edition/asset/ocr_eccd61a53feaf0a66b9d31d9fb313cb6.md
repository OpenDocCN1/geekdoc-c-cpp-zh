# The Divide and Conquer method

The Divide and Conquer method uses multiple links to multiple style sheets on an as-needed basis per page. Start with a link to a file with global styles used by all pages, and then add links to styles used for that page only. For example, if you use a special carousel module only on the main page, it would not go into the global file, but would exist as a separate CSS file for the home page or as a part of a CSS file of general components.

Pros—Mix and match style sheets from your library to load only the styles you need and reduce bloated file sizes. Plus, as long as you keep your files organized, these are generally easier to edit.

Cons—Multiple files mean multiple server calls, which slows downloads. Plus, multiple files can be hard to keep up with, and their cascade order can conflict in unpredictable ways.

![](bbox=[0.08, 0.43, 0.89, 0.87])

The Divide and Conquer method splits the CSS into multiple files, which are then applied only if they are relevant to the page.