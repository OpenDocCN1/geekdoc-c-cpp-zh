10. If you haven't already merged the two h1 selectors, open Styles.css and scroll down to the end of the file. Copy the two lines for the padding and margin properties to the clipboard and then delete the entire selector. Scroll up in the file and then paste the two CSS rules inside the other h1 selector. You should end up with this code:

```
h1
{
    font-size: 20px;
    padding: 0;
    margin: 0 0 10px 0;
}
```

11. Save any pending changes you may have and then open Default.aspx in your browser by pressing Ctrl+F5. Note that the paragraphs haven't changed and still use the same blue and italic font.

# How It Works

Unfortunately, VS doesn't allow you to move inline styles to external style sheet files. However, by creating a copy of the existing style, and then deleting the original inline style, you can achieve the same effect. Moving embedded or external style sheets between files is a lot easier. You can simply drag a style from one file to another, and VS will automatically move the code for you. This makes it extremely easy to organize your CSS. Instead of leaving all your embedded CSS in your page because you're afraid to touch it, you can now simply drag and drop it into an external file. This makes it a lot easier to reuse those styles in other pages, decreasing page size and page bloat, and making your site a lot easier to manage. Obviously, it's important that the file you are moving your CSS to is attached to the pages you're working with.

# PRACTICAL TIPS ON WORKING WITH CSS

Follow these tips to make the most of CSS:

+   - Take some time to familiarize yourself with the many properties that CSS supports. The best way to do this is to create a brand-new page in your Demos folder, create a few HTML elements like <div> and <p> tags, and then simply experiment with all the different properties. By trying out many of the properties on the CSS Properties Grid, you get a feel for what options you have available. This makes it easier later if you want to apply a certain effect to some piece of content.
+   - When creating custom CSS classes, try to come up with names that describe the behavior of the rule, rather than the look and feel. For example, a class called .Introduction to style the first paragraph of a page is a good description. It enables you to change the underlying values without affecting the actual meaning of the name. But classes with names like .BlueAndItalic are guaranteed to give you problems later. What if you decide to change the blue to black later? You either end up with a very odd class name not describing its own