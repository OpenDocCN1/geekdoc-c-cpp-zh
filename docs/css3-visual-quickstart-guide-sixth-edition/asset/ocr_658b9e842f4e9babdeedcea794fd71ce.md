# Styling for a particular language

The World Wide Web is just that—all around the world—which means that anyone, anywhere can see your pages. It also means that Web pages are created in many languages.

The :lang() pseudo-class lets you specify styles that depend on the language specified by the language property.

# To set a style for a specific language:

+   1. Style an element based on its language code. Type the selector (HTML, class, or ID) of the element you want to style, a colon (:), :lang, and enter the letter code for the language you are defining within parentheses (Code 4.9). p:lang(fr) {...}

+   2. The element is styled if it has a matching language code. Set up your tag in the HTML with the language attributes as necessary. <p lang="fr">...</p> If the indicated selector has its language attribute equal to the same value that you indicated in parentheses in Step 1, the style is applied. You can use any string as the language letter code, as long as it matches the value in the HTML. However, the W3C recommends using the codes from RFC 3066 or its successor. For more on language tags, visit www.w3.org/International/articles/language-tags.

> TIP Language styles can go far beyond simple colors and fonts. Many languages have specific symbols for quotes and punctuation, which CSS can add. In Chapter 9, you will find information on how to style quotes for a particular language.