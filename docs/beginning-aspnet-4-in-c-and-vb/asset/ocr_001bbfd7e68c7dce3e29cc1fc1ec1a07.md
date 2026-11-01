# Creating Documents with WPF

# WHAT'S IN THIS CHAPTER?

+   - Creating flow documents
+   - Creating fixed documents
+   - Creating XPS documents
+   - Printing documents

Creating documents is a large part of WPF. The namespace `System.Windows.Documents` supports creating flow and fixed documents. This namespace contains elements with which you can have a rich Word-like experience with flow documents, and create WYSIWYG fixed documents.

*Flow* documents are geared towards screen reading; the content of the document is arranged based on the size of the window, and the flow of the document changes if the window is resized. *Fixed* documents are mainly used for printing and page-oriented content and the content is always arranged in the same way.

This chapter teaches you how to create and print flow and fixed documents, and covers the namespaces `System.Windows.Documents`, `System.Windows.Xps` and `System.IO.Packaging`.

# TEXT ELEMENTS

To build the content of documents, you need document elements. The base class of these elements is `TextElement`. This class defines common properties for font settings, foreground and background, and text effects. `TextElement` is the base class for the classes `Block` and `Inline` whose functionality is explored in the following sections.

# Fonts

An important aspect of text is the look of the text and thus the font. With the `TextElement`, the font can be specified with the properties `FontWeight`, `FontStyle`, `FontStretch`, `FontSize`, and `FontFamily`.

+   - Predefined `FontWeight` values are defined by the `FontWeights` class, which offers values such as `UltraLight`, `Light`, `Medium`, `Normal`, `Bold`, `UltraBold`, and `Heavy`.