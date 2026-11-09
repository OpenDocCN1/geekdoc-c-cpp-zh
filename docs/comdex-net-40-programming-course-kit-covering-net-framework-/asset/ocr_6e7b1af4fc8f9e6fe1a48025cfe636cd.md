**Table 2.18: Noteworthy Properties of the Calendar Control**

| Property | Description |
|---|---|
| `UseAccessibleHeader` | Obtains or sets a value that indicates whether to render the table header `<th>` HTML element for the day headers instead of the table data `<td>` HTML element |
| `VisibleDate` | Obtains or sets the date that specifies the month to display on the Calendar control |
| `WeekendDayStyle` | Obtains the style properties for the weekend dates on the Calendar control |

Noteworthy events of the **Calendar** control are listed in Table 2.19:

**Table 2.19: Noteworthy Events of the Calendar Control**

| Event | Description |
|---|---|
| `SelectionChanged` | Occurs when a user selects a date in the Calendar control |
| `DayRender` | Occurs when each day is displayed in the Calendar control |

+   Perform the following steps to work with the Calendar control:
+   
+   1. *Open* **Visual Studio 2010**.
+   2. *Select* **File > New > Web Site** from the menu bar. The **New Web Site** dialog box opens.
+   3. *Select* **Visual C#** from Installed Templates pane of the **New Web Site** dialog box.
+   4. *Select* **ASP.NET Web Site** in the right pane of the **New Web Site** dialog box.
+   5. *Specify* the location and name of the application in the Web location combo box. In this case, we have provided the name as **CalendarExample**.
+   6. *Click* the **OK** button to save all the settings. The **CalendarExample** application is created (also available on the CD) (Fig.ASP-2.60).
+   7. *Click* the **Design** tab to view the design of the **Default.aspx** page (Fig.ASP-2.60).
+   8. *Add* a **Calendar** control on the Web Form from **Toolbox**, as shown in Fig.ASP-2.60:

![](bbox=[0.316, 0.568, 0.707, 0.791])

Fig.ASP-2.60

The following code snippet is added into the source code of the Web page as soon as the **Calendar** control is placed on the Web Form:

```
```aspx
<asp:Calendar ID="Calendar1" runat="server"></asp:Calendar>
```
```