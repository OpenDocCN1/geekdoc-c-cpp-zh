```
5. Public partial class cookieExample: : System.Web.UI.Page
6. {
7. Protected void Page_Load(object sender, eventargs e)
8. {
9. //------------ Creating Cookie --------------------
//
10. // Creating httpcookie instance by specifying name "student"
11. Httpcookie cokie = new httpcookie("student");
12. // Assigning value to the created cookie
13. Cokie.Value = "Rahul Kumar";
14. // Adding Cookie to the response instance
15. Response.Cookies.Add(cokie);
16. //------------ Fetching Cookie --------------------
//
17. Var co_val = Response.Cookies["student"].Value;
18. Label1.Text = co_val;
19. }
20. }
21. }
```

# Cookie Collection Example:

In the following Example:, we are adding cookie directly to the Cookies collection.

```
// Default.aspx
```