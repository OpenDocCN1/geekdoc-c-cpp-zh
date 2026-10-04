# Using Model Binding with LINQ Queries

Just like the data-bound controls, the ListView has a number of events that fire at specific moments during the control's lifetime. For example, it has ItemInserting and ItemInserted events that fire right before and after an item has been inserted in the underlying data source. You can see more about handling these kinds of events in the next chapter.

Besides the templates, properties, and events you just saw, the ListView control has more to offer. For a detailed explanation of the ListView control and all of its members and behavior, check out the MSDN documentation at http://bit.ly/dCAAw

The next exercise shows you how to put all of this information together. You will see how to define the various templates and the relevant properties to control the look and feel of the ListView control.

# TRY OUT Inserting and Deleting Data with the ListView Control

Inserting items with the ListView can be just as easy as DetailsView: You add the control to the page, define one or more templates (for example, to display an item in read-only mode and another that lets you edit an item), and then use Model Binding to get data from the database and updates back. In this exercise you will see how to use the ListView to add pictures to an album and how to delete pictures again. For now, you will only be able to insert some dummy data into the Picture table, but in a later exercise you will learn how to upload actual pictures, save them on disk, and associate them with the database.

+   2. From the Data category of the Toolbox, draw a ListView control onto the page in the cmpContent placeholder.

+   3. Modify the code for the ListView as:

```
<asp:ListView ID="ListView" runat="server" DataKeyNames="Id"
ItemTemplatePosition="LastItem">
<InsertItemTemplate>
<li>
Description:<asp:TextBox ID="Description" runat="server"
TextMode="Multiline" Text="<%# Bind("Description") %>\></br />
Tooltip:<asp:TextBox ID="Tooltip" runat="server"
Text="<%# Bind("Tooltip") %>\></br />
ImageUrl:<asp:TextBox ID="ImageUrl" runat="server"
Text="<%# Bind("ImageUrl") %>\></br />
<asp:Button ID="InsertButton" runat="server" Text="Insert" CommandName="Insert" />
</li>
</InsertItemTemplate>
<ItemTemplate>
<li>Description:<asp:Label ID="" runat="server"
Text="<%# Eval("Description") %>\></br />
```