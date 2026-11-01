
## FIGURE 13-7
![](img/eadab2ccd79b253c01a3fdff2321202d_513_0.png)

## FIGURE 13-8
![](img/eadab2ccd79b253c01a3fdff2321202d_513_1.png)

![](img/eadab2ccd79b253c01a3fdff2321202d_516_0.png)

## FIGURE 13-10
For some reason, each of your controls may show up twice in the Control ID drop-down list. It doesn't matter which of the DropDownList1 options you choose.

6. Click the Add button to add the selection to the WHERE clause list at the bottom of the screen and click OK.

7. Back in the Configure Data Source wizard, click Next. To test the query, click the Test Query button. If you set up the parameter correctly, a dialog box pops up enabling you to enter a value. Enter a number that you know exists in the Genre table (such as 2) and click OK. If rows exist in the Review table for the chosen genre, they are displayed in the Test Query window. Finally, click Finish to finalize the wizard. If you get a dialog box about refreshing parameters, click Yes to have the code in Markup View updated for you.

8. Save all your changes and open Reviews.aspx in your browser.

> **COMMON MISTAKES** If you get an error stating that the "input string was not in a correct format," ensure that you set the Value of the static ListItem in the drop-down list to an empty string ("") as shown in the preceding exercise.

9. Select a new item in the drop-down list. The page refreshes, and now shows the reviews that belong to the chosen genre. If the page doesn't refresh, ensure that you set AutoPostBack to True in the previous exercise. At this stage the page looks rather messy because the GridView contains many columns but in the next Try It Out you see how to fix this.

2. At this stage, VS has created columns for the GridView in Markup View. To remove those items and define your own, open the Smart Tasks panel for the GridView and click Edit Columns. This brings up the Fields dialog box. If the Selected Fields list contains items, use the Delete button (with the big X) to clear the list first.

3. In the Available Fields list, select Authorized under BoundField (not the one under CheckBoxField) and then click the Add button to copy the item to the Selected Fields list. Repeat this step for the CreateDateTime field. Your dialog box now looks like Figure 13-12.

![](img/eadab2ccd79b253c01a3fdff2321202d_520_0.png)

FIGURE 13-12

4. In the Available Fields at the top of the screen, select HyperLinkField and then click the Add button to add the item to the Selected Fields list as well. Move the HyperLinkField to the top of the list by clicking the button with the up arrow twice. Then, using the Properties Grid on the right, set the following properties on the HyperLinkField:

| PROPERTY | SET ITS VALUE TO |
|---|---|
| HeaderText | Title |
| DataNavigateUrlFields | Id |
| DataNavigateUrlFormatString | AddEditReview.aspx?Id={0} |
| DataTextField | Title |

5. In the list with Available Fields, click CommandField and click the Add button again. Then set the HeaderText of the item you just inserted to Delete and ShowDeleteButton to True using the Properties Grid. This enables you to delete reviews from the database using the GridView later. The Fields dialog box should now look like Figure 13-13.

![](img/eadab2ccd79b253c01a3fdff2321202d_521_0.png)

FIGURE 13-13

6. Click the Authorized column in the Selected Fields list and then click the blue Convert This Field into a TemplateField link visible at the bottom-right of the dialog box in Figure 13-13.
7. Click the CreateDateTime column on the left and set its DataFormatString property to {0:g}.
8. Click OK to apply the changes to the source code.
9. Switch to Markup View and remove the <EditItemTemplate> for the Authorized field. The GridView displays reviews only in read-only mode, so you don't need this template.
10. Modify the Label control in the ItemTemplate of the Authorized field so it ends up like this:
<asp:Label ID="AuthorizedLabel" runat="server" Text='<%# GetBooleanText(Eval("Authorized")) %>' />
11. Switch to the Code Behind of the page by pressing F7 and add the following function—which returns the text Yes or No depending on the boolean value that you pass—to the top of the class file, right after the Inherits line in VB.NET and after the opening curly brace in C#.

### VB.NET

```
Inherits System.Web.UI.Page
Protected Function GetBooleanText(booleanValue As Object) As String
    Dim authorized As Boolean = CType(booleanValue, Boolean)
    If authorized Then
        Return "Yes"
```

The `HyperLink` for the `Title` column that you set up points to a page called `AddEditReview.aspx`. This page enables you to create new and update existing reviews. You see how to create this page in the following section.

## UPDATING AND INSERTING DATA

Earlier in this chapter I discussed how to do simple updates with the `GridView` and the `SqlDataSource` controls. Although this built-in update behavior is fine in many circumstances, it is not always extensive enough to meet all your demands.

Fortunately, controls like `FormView` and `DetailsView` enable you to tweak their look and feel, giving you a lot more flexibility in the way your end users work with their data. In the next section you see how to use the `DetailsView` to give the user a much easier interface to insert and edit reviews in the database.

### Using DetailsView to Insert and Update Data

Earlier in this chapter you learned how to set up a simple `DetailsView` control and fully rely on VS and the control itself to render the relevant user interface in the browser. Obviously, this default behavior is often not enough. What if you wanted to influence the controls used in the interface? For example, what if you wanted to use a `DropDownList` instead of a simple `TextBox` for the genre? And what if you wanted to add one or more validation controls that you learned about in Chapter 9? Or what if you wanted to manage some of the data being sent to the database programmatically? All of this is possible with the `DetailsView` control, its template-based columns, and the numerous events that the control fires at various stages in its life cycle.

First, however, you need to learn a bit more about the different events that the data-bound and data source controls fire. The following table lists some of the events that the `DetailsView`, the `FormView`, and the `ListView` expose and raise during their lifetime. The `GridView` has similar events, but they start with `Row` instead of `Item`. Because the `DataList` and `Repeater` controls do not natively support editing of data, they do not have any of these events.

| EVENT | DESCRIPTION |
|---|---|
| `ItemInserting` | Fires right before the `Insert` command is executed against the data source. This is an ideal location to change the data that is about to be sent to the database. |
| `ItemInserted` | Fires right after the `Insert` command has been executed against the data source. |
| `ItemUpdating` | Fires right before the `Update` command is executed against the data source. This is an ideal location to change the data that is about to be sent to the database. |
| `ItemUpdated` | Fires right after the `Update` command has been executed against the data source. |
| `ItemDeleting` | Fires right before the `Delete` command is executed against the data source. |
| `ItemDeleted` | Fires right after the `Delete` command has been executed against the data source. |

```
<asp:TextBox ID="TextBox2" TextMode="MultiLine" Width="500" Height="100" runat="server" Text='<%# Bind("Summary") %>'></asp:TextBox>
<asp:RequiredFieldValidator ControlToValidate="TextBox2" runat="server" ErrorMessage="Enter a summary"></asp:RequiredFieldValidator>
</InsertItemTemplate>
<ItemTemplate>
<asp:Label ID="Label2" runat="server" Text='<%# Bind("Summary") %>'></asp:Label>
</ItemTemplate>
</asp:templatefield>
```

The Title and Body fields should look similar to Summary. The TextBox for the Title field doesn't have the TextMode, Width, and Height properties applied, whereas the Body field is missing the RequiredFieldValidator. Other than that, the fields should look pretty similar to the Summary field.

5. Switch to Design View and drag a new SqlDataSource control next to SqlDataSource1 that is already on the page. Open the new control's Smart Tasks panel and click Configure Data Source. Select the Planet Wrox connection string from the drop-down list and click Next. Select the Id and Name columns from the Genre table and set up an ORDER BY clause on the SortOrder column by clicking the ORDER BY button and choosing SortOrder from the Sort By drop-down list. When you click OK, the Configure Data Source screen looks like Figure 13-19.

![](img/eadab2ccd79b253c01a3fdff2321202d_530_0.png)

FIGURE 13-19
