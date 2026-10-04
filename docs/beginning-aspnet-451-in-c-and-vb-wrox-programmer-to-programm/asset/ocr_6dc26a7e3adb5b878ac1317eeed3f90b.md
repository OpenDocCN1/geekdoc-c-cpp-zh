# CHAPTER 3 DESIGNING YOUR WEB PAGES

![](bbox=[0.105, 0.098, 0.613, 0.313])

Figure 3-2

Although this black-and-white book makes it difficult to see different font colors, in Figure 3-2 you can see clearly that the <h1> has a larger font size. The figure also shows that all paragraphs are now displayed with the right of the window, because the class attribute is set to RightAligned.

> COMMON MISTAKES If you don't see the last paragraph glued to the right border of the Document Window, make sure you typed RightAligned exactly the same in the <style> tag and the class attribute. Because CSS is case sensitive, there is a big difference between RightAligned and rightaligned.

+   6. Press Ctrl+F5 to view CssDemo.asmx in your browser. The page in the browser is identical to the preview you got in the Design View of VS.

# How It Works

Although the code you typed in exercise is relatively simple, there's a lot going under the hood of the browser (and the Design View of VS) to make this possible. You started by adding some styles to the <head> section of the page:

```
<style>
h1 {
  font-size: 20px;
  color: Green;
}
</style>
```

The <style> tag is used to wrap a CSS style sheet that is embedded in the page.
The code block from h1 until the closing curly brace } between the <style> tags is called a rule or simply a rule. The rule in this code snippet defines the appearance for all <h1> elements in your page. The h1 at the top of the code block is called a selector and is used to indicate to what element the