# Getting Some Input from the User 669

```
2. Listbox<br />
<asp:ListBox ID='ListBox1' runat='server">
  <asp:ListItem>Item 1</asp:ListItem>
  <asp:ListItem>Item 2</asp:ListItem>
  <asp:ListItem>Item 3</asp:ListItem>
  <asp:ListItem>Item 4</asp:ListItem>
</asp:ListBox>
</div>
</form>
<body>
</html>
```

# Using other kinds of input controls

ASP.NET provides a number of other input types that are combinations of the above, or are nontraditional inputs. (See Figure 3-5) They are all special controls, you need to be in your toolbox so you can use them when the need arises.

![](bbox=[0.238, 0.423, 0.843, 0.725])

Figure 3-5: The stragglers.

They include the following inputs:

+   * **FileUpload:** The FileUpload does exactly what it says. It creates an HTML input of type **File** and makes the form enctype (encoding type) into multipart form-data. This allows the Web server to accept a long stream of binary data, which you can capture with a streamer.
* **Imagenaps:** Imagemaps are nearly relics of a bygone era. Essentially, they allow you to mark off pixel by pixel maps on top of images and then assign regions within those maps to URLs or other actions.