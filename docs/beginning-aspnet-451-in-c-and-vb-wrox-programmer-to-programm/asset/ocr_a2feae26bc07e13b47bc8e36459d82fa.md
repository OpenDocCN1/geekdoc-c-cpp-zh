2. At this stage, VS has created columns for the GridView in Markup View. To remove items and define your own, use the Smart Tasks panel for the GridView and click Edit Columns. This brings up the Fields dialog box. If the Selected Fields contains items, use the Delete button (with the big X) to clear the first.

3. In the Available list, select BoundField (not the one under CheckField) and click the Add button to add it to the Selected Fields list. Repeat this step for the CreateTime field. Your dialog box now looks like Figure 13-12.

![](bbox=[0.112, 0.255, 0.687, 0.618])

FIGURE 13-12

4. In the Available Fields at the top of the screen, select HyperLinkField and then click the Add button to add it to the Selected Fields list as well. Move the HyperLinkField to the top of the list by clicking the button with the up arrow. Then, using the Properties Grid on the right, set the following properties on the HyperLinkField:

| PROPERTY | SET IT VALUE TO |
| --- | --- |
| HeaderText | Title |
| DataNavigateUrlFields | Id |
| DataNavigateUrlFormatString | AddEditReview.aspx?Id={0} |
| DataTextField | Title |