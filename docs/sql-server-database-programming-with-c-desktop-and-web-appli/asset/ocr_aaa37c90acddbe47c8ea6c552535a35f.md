# Data Selection Query with Visual#.NET

| RTOS Project | CourseForm() |

```
```csharp\using System.Data;
using System.Data.SqlClient;
using System.Data.OleDb;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace RTOS_Project
{
    public class CourseForm : Form
{
        LogForm login = new LoginForm();
        public CourseForm()
        {
            InitializeComponent();
            ComboName.Items.Add("Ying Bai");
            ComboName.Items.Add("Davis Bhalla");
            ComboName.Items.Add("Black Anderson");
            ComboName.Items.Add("Steve Johnson");
            ComboName.Items.Add("Jenney King");
            ComboName.Items.Add("Alice Brown");
            ComboName.Items.Add("Dusty Angel");
            ComboName.Items.Add("Jeff Henry");
            ComboMethod.SelectedIndex = 0;
            ComboMethod.Items.Add("DataAdapter Method");
            ComboMethod.Items.Add("DataReader Method");
        }
    }
}
```
```

FIGURE 5.80 The codes is for the constructor of CourseForm.

+   C. All eight faculty members are added into the Faculty Name combo to enable users to select one of them to perform query for that faculty member.
D. The SelectedIndex = 0 makes the first faculty member in the Faculty Name combo as a default.
E. Two different methods, DataAdapter Method and DataReader Method, are added into the Query Method combo to enable users to select one of them to perform the related query. The first query, DataAdapter Method, is selected as the default method by setting the SelectedIndex property to 0.

The next job is for the Select button click (course_id) taught by the selected faculty in the Course form. Generally, we need to use two queries to retrieve all courses because there is no faculty name column available in the Course, and each course course_id is related to a faculty_id in the Course table. In order to get a faculty_id that is associated with the selected faculty, we must first perform a query to the Faculty table to obtain it. To simplify this data action, a join query is used in this method and it is a desired method to complete its functionality.

# 5.15.6.1 Retrieve Data From Multiple Tables Using the Joined Tables

To have a clear picture why we need to use the Join query method for this data action, let's first take a look at the data in our sample database. A part of Faculty and Course table in the CSE_DEPT database is shown in 5.81.
The faculty_id in the Faculty is a primary key, but it is also a foreign key in the Course table. The relationship between the Faculty and the Course table is one-to-many. What we want to is