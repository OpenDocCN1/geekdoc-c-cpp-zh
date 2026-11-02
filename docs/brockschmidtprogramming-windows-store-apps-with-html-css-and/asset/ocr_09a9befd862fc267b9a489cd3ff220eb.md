# Fonts and Text Overflow

As discussed earlier, typography is an important design element for Store apps, and for the most part the standard font styles using Segoe UI are already defined in the default WinJS stylesheets. In the Windows SDK there is a very helpful CSS typography JS sample that compares the HTML header elements and the win-type-* styles, demonstrating font fallbacks and how to use bidirectional fonts (left to right and right to left directions).

Speaking of fonts, custom fonts resources using the @font-face rule in CSS are allowed in Store apps. For local context pages, the src property for the rule must refer to an in-package font file (that is, a URI that begins with / or ms-appx:///). Pages running in the web context can load fonts from remote sources. Blend for Visual Studio 2013 supports this directly. First import a font into your project in Blend: right-click a project folder in the Project tab and select Add Existing Item, navigate to your font file, and press OK. As soon as you do so, Blend will bring up a series of two dialog boxes asking if you'd like to create an @font-face rule:

![](bbox=[0.13, 0.53, 0.55, 0.65])

![](bbox=[0.13, 0.66, 0.55, 0.9])