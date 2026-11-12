# ★ Not styling an element

So far you've looked at ways to style a tag if it /s something. The negation selector, :not, allows you to not style something for a particular selector.

# To not set a style for a particular element:

+   1. Style elements to exclude certain selectors. Type the selector (HTML, class, or ID) of the element you want to style, a colon (:), not, and enter the selectors you want excluded from this rule in parentheses (Code 4.10).
+   
+   `p:not(.dialog) {...}`

+   2. The element is not styled if it contains the indicated selector.
+   
+   `<p class="dialog">...</p>
+   <p>...</p>`

The styles are applied to elements that match the initial selector but not the selector in parentheses.