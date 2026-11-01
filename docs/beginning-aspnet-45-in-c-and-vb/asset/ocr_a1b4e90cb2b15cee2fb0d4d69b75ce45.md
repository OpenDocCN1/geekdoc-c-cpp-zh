2. At this stage, VS has created columns for the GridView in Markup View. To remove those items and define your own, open the Smart Tasks panel for the GridView and click Edit Columns. This brings up the Fields dialog box. If the Selected Fields list contains items, use the Delete button (with the big X) to clear the list first.

3. In the Available Fields list, select Authorized under BoundField (not the one under CheckBoxField) and then click the Add button to copy the item to the Selected Fields list. Repeat this step for the CreateDateTime field. Your dialog box now looks like Figure 13-12.

![](bbox=[0.15, 0.33, 0.78, 0.72])

FIGURE 13-12

4. In the Available Fields at the top of the screen, select HyperLinkField and then click the Add button to add the item to the Selected Fields list as well. Move the HyperLinkField to the top of the list by clicking the button with the up arrow twice. Then, using the Properties Grid on the right, set the following properties on the HyperLinkField:

| PROPERTY | SET ITS VALUE TO |
|---|---|
| HeaderText | Title |
| DataNavigateUrlFields | Id |
| DataNavigateUrlFormatString | AddEditReview.aspx?Id={0} |
| DataTextField | Title |

5. In the list with Available Fields, click CommandField and click the Add button again. Then set the HeaderText of the item you just inserted to Delete and ShowDeleteButton to True using the