# Creating a Crosstab View with Multiple Value Fields

3. Under each field in the Crosstab row, select whether the field will be a row heading, a column heading, or a value.
4. Run the query to see your crosstab in action.

When building your crosstab in the query design grid, keep the following in mind:

+   - You must have a minimum of one row heading, one column heading, and one value field.
+   - You can't define more than one column heading.
+   - You can't define more than one value heading.
+   - You are not limited to only three row headings.

One of the rules of a Crosstab query is that you cannot have more than one Value field. However, there is a trick to work around this limitation and analyze more than one metric with the same data groups.

Start by creating the Crosstab query shown in the following figure. Note that your Column heading is a custom field that will give you the region name and the word "Revenue" next to it.

![](bbox=[0.12, 0.68, 0.88, 0.85])

Next, create another crosstab query as shown in the following figure and save it as Crosstab-2. Again, your column heading is a custom field that will give you the region name and the word Transactions next to it.