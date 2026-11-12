# To determine the cascade-order value for an element:

Collect all styles that will be applied to the element. Find all the inherent, applied, and inherited styles that will be applied to the element, and then use the following criteria to determine which styles are applied in the cascade order, with the criteria at the top being most important A

+   1. User styles
+   Most Web browsers allow users to specify their own default style sheets. In principle, these always have precedence over other styles.

+   2. Inline styles
+   If the style is inline (see Chapter 3), it is always applied regardless of all other factors. That's why you should never use them in your final HTML code.

+   3. Media type
+   Obviously, if the media type is set for a style and element that is not being displayed in that media type, the style will not be used.

+   4. Importance
+   Including !important with a declaration gives it top billing when displayed. (See “Making a Declaration Important” in this chapter.)
+   
+   Many browsers let users define their own style sheets for use by the browser. If both the page author and the visitor have included !important in their declarations, the user's declaration wins.
+   
+   In theory, an author's style sheets override a visitor's style sheets unless the visitor uses the !important value. In practice, however, most browsers favor a user's style sheet when determining which declarations are used for a tag.

![](bbox=[0.535, 0.082, 0.94, 0.48])

A The cascade order from most important to least important.