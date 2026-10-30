
Be sure to restore the Echo On status to Yes at the end of the macro so that Access resumes its normal appearance. If Echo On is not set back to Yes, the user may think the application has "locked up" because of a problem.

- OpenQuery: This action is the heart of the mcrBackupContactsAndProducts macro. OpenQuery opens a select or crosstab query or runs an action query. The Query Name argument contains the name of the query to open or run. The View argument lets you pick the view—Datasheet, Design, Print Preview, and so forth—for a select or crosstab query. The Data Mode argument lets you choose from Add, Edit, or Read Only to limit what users can do in a select query. The View and Data Mode arguments are ignored for action queries.

## NOTE

You could easily build this macro just using the four OpenQuery actions, but running it would be cumbersome, requiring the user to watch the macro run through each query and be ready to confirm each query action. The DisplayHourglassPointer, SetWarnings, Echo, and MessageBox actions serve to eliminate the need for user interaction and let the user know when the macro has completed its activity.

## Submacros

When automating your application with macros, you might easily get carried away filling the Navigation pane with a bunch of little macros for opening every form and every report. If you have a series of actions that are performed in a number of places, ideally you only want one copy, so that you need to make changes only in one place. Submacros give you that capability: You define the series of actions in one place as a submacro, and then invoke that submacro wherever it's needed.

The macro action drop-down list contains Submacro as an entry. While working on a macro, selecting Submacro from the action list adds an area to the macro where you can input the actions associated with the submacro.

Without using submacros, you'd have to create three separate macros to automate a main menu form with three buttons that open frmContacts, frmProducts, and frmSales. Using submacros, just create a single top-level macro that contains three submacros. Each of the submacros opens one form. Only the top-level macro appears in the Navigation pane. Table 22.2 shows the submacro names, the actions, and submacro actions for mcrMainMenu.

## TABLE 22.2 mcrMainMenu

| Submacro | Action | Action Argument | Action Argument Setting |
|---|---|---|---|
| OpenContacts | OpenForm | Form Name | frmContacts |
|  |  | View | Form |
|  |  | Filter Name | <Leave Blank> |
|  |  | Where Condition | <Leave Blank> |
|  |  | Data Mode | <Leave Blank> |
|  |  | Window Mode | Normal |
| OpenProducts | OpenForm | Form Name | frmProducts |
|  |  | View | Form |
|  |  | Filter Name | <Leave Blank> |
|  |  | Where Condition | [ProductID] >3 |
|  |  | Data Mode | Read Only |
|  |  | Window Mode | Dialog |
| OpenSales | OpenForm | Form Name | frmSales |
|  |  | View | Layout |
|  |  | Filter Name | qrySales2012 |
|  |  | Where Condition | <Leave Blank> |
|  |  | Data Mode | Edit |
|  |  | Window Mode | Icon |

Figure 22.9 shows the creation of mcrMainMenu in progress. The developer has selected Submacro from the Add New Action list, provided a name (OpenContacts) for the submacro, and filled in its properties.

## FIGURE 22.9

Adding a second submacro to a macro.

![](img/1e45673ab6eca9d20e67635ff5b9b318_760_0.png)

## Tip

The Add New Action drop-down displays a list of available actions sorted alphabetically. However, the first four items—Comment, Group, If, and Submacro—are shown at the top of the list rather than in their proper place. These four items are really program flow elements and are separated from the items considered actions.

Next, the developer selected Submacro a second time from the Add New Action list, and provided OpenProduct as its name. None of the arguments for the second submacro has been filled in.

The confusing thing about submacros is that you see two Add New Action lists in Figure 22.9. One is at the very bottom of the main macro, while the second is inside the second submacro. The submacro that is currently being developed (OpenProducts) is enclosed in a lightly shaded box, while the completed submacro (OpenContacts) at the top of the main macro is not contained in a box.

## NOTE

In Figure 22.9, notice the small minus sign to the left of Submacro in the first line of the macro. The minus sign is there to show you that the submacro is currently expanded so that you can see all the steps in the submacro. Clicking the minus sign collapses the macro to a single line, which lets you view more of the macro and its actions in a single glance. Several figures in this chapter show macros with portions collapsed (identifiable by the small plus sign to the left), so don’t be confused if portions of a macro illustrated in a figure appear to be missing.

To implement a macro using submacros, create a form (frmMainMenu) with three buttons—in this case, cmdContacts, cmdProducts, and cmdSales. Then set the On Click event properties of these buttons as follows (see Figure 22.10):

| Button Name | On Click Event Property |
|---|---|
| cmdContacts | mcrMainMenu.OpenContacts |
| cmdProducts | mcrMainMenu.OpenProducts |
| cmdSales | mcrMainMenu.OpenSales |

Open frmMainMenu in Form view and click the Contacts button; frmContacts opens and displays all the records. Click the Products button to display frmProducts, which only displays one record. Click the Sales button to display frmSales in a minimized state, which displays the sales made in 2012.

To see why these forms open differently, take a look at the action arguments for the OpenForm action:

- Form Name: This argument is the name of the form you want the macro to open.
- View: This argument lets you select which view to open the form in: Form, Design, Print Preview, Datasheet, PivotTable, PivotChart, or Layout. For this example,

frmContacts and frmProducts open in Form view, while frmSales opens in Layout view.

- **Filter Name:** This argument lets you select a query or a filter saved as a query to restrict and/or sort the records for the form. For this example, this argument is set to qrySales2012 for the OpenSales macro. qrySales2012 is a query that outputs all the fields in the table and only displays sales between 1/1/2012 and 12/31/2012. This query also sorts the records by SaleDate.
- **Where Condition:** This argument lets you enter a SQL Where clause or expression that selects records for the form from its underlying table or query. For this example, this argument is set to [ProductID] = 3 for the OpenProducts submacro, which only shows one record when you open frmProducts.
- **Data Mode:** This argument lets you choose the data-entry mode for the form. Select Add to only allow users to add new records, Edit to allow adding and editing of records, or Read Only to allow only viewing of records. This setting only applies to forms opened in Form view or Datasheet view, and overrides settings of the form's AllowEdits, AllowDeletions, AllowAdditions, and DataEntry properties. To use the form's setting for these properties, leave this argument blank. For this example, frmProducts opens in read-only mode, while frmContacts and frmSales allow editing.
- **Window Mode:** This argument lets you choose the window mode for the form. Select Normal to use the form's properties. Select Hidden to open the form with its Visible property set to No. Select Icon to open the form minimized. Select Dialog to open the form with its Modal and PopUp properties set to Yes and Border Style property set to Dialog. For this example, frmContacts opens normally, frmProducts opens as a dialog box, and frmSales opens minimized.

## FIGURE 22.10

The submacro names appear after the macro object in the event property drop-down list.

![](img/1e45673ab6eca9d20e67635ff5b9b318_762_0.png)
