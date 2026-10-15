```
<br />
<asp:Button ID="Button1" runat="server" onclick="Button1_Click" style="margin-left: 185px" Text="Display" Width="131px" />

</div> </div>

</div>
</form>
</body>
</html>
```

After modifying the code in the source file, let us now change the code in the code-behind file of the Default.aspx page, as shown in Listing 27.31:

# Listing 27.31: Showing the Code for the Code-Behind File of the Default.aspx Page

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
public partial class _Default : System.Web.UI.Page{
    protected void Page_Load(object sender, EventArgs e) {
    }
    protected void Button1_Click(object sender, EventArgs e) {
        var numbers = from n in Enumerable.Range(1, 50)
        select new { Number = n, OddEven = n % 2 == 1 ? "odd" : "even" };
        foreach (var n in numbers) {
            ListBox1.Items.Add("The number is " + n.Number + n.OddEven);
        }
    }
}
```

Now, let’s run the application by pressing the F5 key on the keyboard. When you click the Display button, the output of the application is as shown in Figure 27.21:

![](bbox=[0.25, 0.53, 0.78, 0.91])

Figure 27.21: Displaying the Output of the GenerationOperators Application