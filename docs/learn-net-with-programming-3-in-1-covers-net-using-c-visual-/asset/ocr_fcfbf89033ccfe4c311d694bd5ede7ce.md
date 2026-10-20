+   1. <%@ Page Title="Home Page" Language="C#" autoeventwireup="true" codebehind="Default.aspx.cs"
+   2. Inherits="coockieExample:_Default" %>
+   3. <form id="form1" runat="server">
+   4. <asp:Label ID="Label1" runat="server" Text="Select Brand Preferences"></asp:Label>
+   5. <br />
+   6. <br />
+   7. <asp:checkbox ID="apple" runat="server" Text="Apple" />
+   8. <br />
+   9. <asp:checkbox ID="dell" runat="server" Text="Dell" />
+   10. <br />
+   11. <asp:checkbox ID="lenevo" runat="server" Text="Lenevo" />
+   12. <br />
+   13. <asp:checkbox ID="acer" runat="server" Text="Acer" />
+   14. <br />
+   15. <asp:checkbox ID="sony" runat="server" Text="Sony" />
+   16. <br />
+   17. <asp:checkbox ID="wipro" runat="server" Text="Wipro" />
+   18. <br />
+   19. <br />
+   20. <asp:Button ID="Button1" runat="server" onclick="Button1_Click" Text="Submit" />