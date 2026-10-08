# TABLE 20-11: Selectors Supported by jQuery

| SELECTOR | DESCRIPTION |
| --- | --- |
| #id | Returns the first element, if any, in the DOM with a matching id attribute. |
| element | Returns all elements with a matching element name. |
| .class | Returns all elements with a matching CSS class. |
| * | Returns all elements in the page. |
| selector1, ..., selectorN | Applies given basic selectors, and returns the combined results. |
| parent > child | Given a selector, returns the collection of all elements that match the child selector. |
| ancestor descendant | Given an ancestor selector, returns the collection of all descendant elements that match the descendant selector. The descendant does not have to be a grandchild or even a more derived element in the hierarchy. |
| prev + next | Given a selector, returns the collection of all sibling elements that match the next selector and are located next to the prev selector. |
| prev - sibling | Given a selector, returns the collection of all sibling elements that match the sibling selector and follows the prev selector. |

Most queries selectors are composed with filters. Table 20-12 summarizes the filters you can use in jQuery.

# TABLE 20-12: Filters in jQuery

| FILTER | DESCRIPTION |
| --- | --- |
| :first | Returns the first element of the selected collection of elements. |
| :last | Returns the last element of the selected collection of elements. |
| :not(selector) | Filters out elements matching the specified selector. |
| :even | Returns all even elements in the selected collection. |
| :odd | Returns all odd elements in the selected collection. |
| :nth-child(expr) | Returns all children of any parent that match the given expression. The expression can be an index or a sequence (for example, 4n+3), including standard sequences (such as odd and even). |