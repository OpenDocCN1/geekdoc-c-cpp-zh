```
```html
<asp:textbox ID="txtsecretvalue" runat="server" />
<br />
<br />
<input id="Button1" type="button" value="button" Onclick="changehiddenvalue()" />
<asp:Button ID="btnpost" runat="server" Text="Post" />
<br />
<br />
<asp:Label ID="lblsecretvalue" runat="server" />
</div>
</form>
</body>
</html>
```
```

The HTML button calls the changehiddenvalue function, highlighted in the code listing. This function has two alert methods that are helpful in debugging; they can be omitted or commented out.

Changehiddenvalue demonstrates two equivalent ways of getting a reference to a control on the page, both using the javascript getelementbyid method. This method.