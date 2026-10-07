# Accessing Data in ASP.NET

| WebLINQSQL_Course Project | Page_Load(object sender, EventArgs e) |

```
using System;
using System.Linq;
namespace SQLWebSelect_Project
{
    public partial class Course : System.Web.UI.Page
    {
        WebLINQSQL_Project.CSE_DEPTDataContext c_dept = new WebLINQSQL_Project.CSE_DEPTDataContext();
        protected void Page_Load(object sender, EventArgs e)
        {
            if (IsPostBack)
            {
                CurrentFaculty();
                ComboName.SelectedIndex = 0;
            }
            void CurrentFaculty()
            {
                ComboName.Items.Clear();
                var faculty = (from fi in c_se_dept.Faculties
                              let fields = "Faculty_name"
                              select fi);
                foreach (var f in faculty)
                    ComboName.Items.Add(f.faculty_name);
            }
        }
}
```

**FIGURE 8.75** Initialization codes for the faculty web page.

| WebLINQSQL_Course Project | cmdSelect_Click(object sender, EventArgs e) |

```
protected void cmdSelect_Click(object sender, EventArgs e)
{
    var c_info = from ci in c_se_dept.Courses
                 join fi in c_se_dept.Faculties on ci.faculty_id equals fi.faculty_id
                 where (fi.faculty_name == ComboName.Text)
                 select ci;
    CourseList.Clear();
    foreach (var cid in c_info)
        CourseList.Items.Add(cid.course_id);
}
```

**FIGURE 8.76** The codes for the Data Selection Query

# **8.8.1.2 The Coding for this method**

The function of this method is: when the user selected a desired faculty member from the Faculty Combobox clicks the Select button, all course_id related to courses taught by the selected faculty member should be retrieved from the database and displayed in the list box CourseList on the page.

Double-click on the Select button from the Design View of the Course page to open its Click method, and enter the codes that are shown in Figure 8.76 into this method.
Let's take a close look at these pieces of code to see how it works.

+   An inner LINQ query is generated first to define the relationships between the Course and the Faculty tables in our sample database. As we know, there is no faculty_name column available in the Course table, and the only column related to the Faculty table is the