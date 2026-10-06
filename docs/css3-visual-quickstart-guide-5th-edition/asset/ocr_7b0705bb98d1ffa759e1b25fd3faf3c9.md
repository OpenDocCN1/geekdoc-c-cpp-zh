# Putting It All Together

+   1. Add content to your HTML file. Using the HTML file you created in chapter 2, add text and image content. I tend to use Alice's Adventures in Wonderland, but anything will do. A great source for text is Project Gutenberg (www.gutenberg.org).

+   2. Mark up your content. All styles require markup in the Web page to give them something to be applied. Make sure to tag headers and paragraphs.

+   3. Add classes and IDs to your markup. Classes give you a "hook" to apply specific styles to specific elements. Don't go overboard, though. Only add classes where it useful to differentiate kinds of elements and IDs to differentiate a specific element in the design.

+   4. Add your HTML, class, and ID declarations to the head of your document in `<style>`. You can style these however you see fit, based on the the styles presented in chapters 5-12.

+   5. Add comments to your CSS code. The note can include information about the code, or contact information about the creator (you) and how to contact them with questions.

+   6. Move your embedded styles from step 4 into an external file. Create the text file and then copy and paste just the CSS code (everything between but not including the `<style>` tags) into the text file. Make sure to save the file with a .css extension.

+   7. Add a `<link>` from the external style sheet. When you test your Web page in a browser, it should look just like it it did on Step 4, but no the CSS is accessible to all of your Web pages.