# ## Augmenting field values with your own text

You can augment the values in your fields by adding your own text. For example, you may want to concatenate the row values of the Type field and the Code field but separate them with a colon. The query in Figure 11.16 does just that.

# ### FIGURE 11.16

This query concatenates the row values of the Type field and the Code field and separates them with a colon.

![](bbox=[0.168, 0.409, 0.4, 0.625])

Take a moment to analyze the following query breakdown:

+   - **[Type]:** This tells Access to use the row values of the Type field.
+   - **&:** The ampersand is a character operator that joins strings together.
+   - **":":** This text will add a colon to the concatenated string.
+   - **&:** The ampersand is a character operator that joins strings together.
+   - **[Code]:** This tells Access to use the row values of the Code field.

Figure 11.17 shows the results of this query.

> **NOTE**
> 
> When specifying your own text in a query, you must enclose the text in quotes. You can concatenate numeric data without the quotes.