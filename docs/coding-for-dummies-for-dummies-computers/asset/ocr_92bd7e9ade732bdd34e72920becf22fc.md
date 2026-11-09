# Styling (More) Elements on Your Page

In this section, you discover common ways to style lists and tables. In the previous chapter, the CSS properties and values you learned like color and font-family can apply to any HTML element containing text. By contrast, some of the CSS shown here is used only to style lists, tables, and forms.

# Styling lists

In Chapter 5 you learned how to create ordered lists, which start with markers like letters or numbers, and unordered lists, which start with markers like bullet points. By default, list items in an ordered list use numbers (for example, 1, 2, 3), whereas list items in unordered lists use a solid-black-circle (●).

These defaults may not be appropriate for all circumstances. In fact, the two most common tasks when styling a list include:

+   - **Changing the marker used to create a list:** For unordered lists, like this one, you can use a solid disc, empty circle, or square bullet point. For ordered lists, you can use numbers, roman numerals (upper or lower case), or case letters (upper or lower).
+   - **Specifying an image to use as the bullet point:** You can create your own marker for ordered and unordered lists instead of using the default option. For example, if you created an unordered bulleted list for a burger restaurant, instead of using a solid circle as a bullet point you could use a color hamburger icon image.

You can accomplish either of these tasks by using the properties in Table 7-1 with an ol or ul selector to modify the list type.

CSS selectors using properties and rules modify HTML elements by the same name. For example, Figure 7-1 has the HTML <ul> tags that are referred to in CSS with the ul selector, and styled using the properties and rules in Table 7-1.

![](bbox=[0.118, 0.639, 0.204, 0.713])

| Table 7-1 | Common CSS Properties and Values for Styling Lists | |
|---|---|---|
| **Property Name** | **Possible Values** | **Description** |
| list-style-type (unordered list) | disc<br>circle<br>square<br>none | Sets the markers used to create list items in an unordered list to disc (●), circle (○), square (■), or none. |