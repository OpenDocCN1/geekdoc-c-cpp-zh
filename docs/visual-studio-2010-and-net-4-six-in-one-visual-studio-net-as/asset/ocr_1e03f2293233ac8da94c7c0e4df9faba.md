```
<div class="display-field">
  %: String.Format("{0:g}", Model.Published) %></div>
<div class="display-label">Publisher</div>
<div class="display-field">%: Model.Published %></div>
</fieldset>
<p>
  %: Html.ActionLink("Edit", "Edit", new ( id=Model.Id )) %>
  %: Html.ActionLink("Back to List", "Index") %>
</p>
</asp:Content>
```

Code file [Book/Details.aspx] available for download at Wrox.com.

Build the project and start by pressing Ctrl+F5. From the home page, navigate to the list of books, and click on the Details link of any book displayed in the list. The page with the book attributes appears in your browser, as shown in Figure 18-19.

![](bbox=[0.147, 0.406, 0.715, 0.908])

FIGURE 18-19: The details of a book