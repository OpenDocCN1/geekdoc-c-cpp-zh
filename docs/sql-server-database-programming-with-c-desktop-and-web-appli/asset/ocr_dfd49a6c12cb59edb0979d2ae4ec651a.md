# Data Inserting with C#.NET

| cmdInsert_Click(object sender, EventArgs e) |

```
private void cmdInsert_Click(object sender, EventArgs e)
{
    int count = 0; InsertCount = 0;
    CSE_DEPTData..Course.NewCourseRow();
    CSE_DEPTData..TableAdapters.FacultyTableAdapter.FacultyTableAdapter = 
        new CSE_DEPTDataSet.TableAdapters.FacultyTableAdapter();

    InitCourseInfo();
    BC count = CheckCoursesInfo();
    if (count == 0)
    {
        FacultyTableAPT.TableAdapter.FindFacultyIDByName(ComboName.Text);
        if (ComboMethod.Text == "Table Insert")
        {
            int insertCount = tableAdapter.InsertCourse(txtID, txtCourseName.Text,
                Convert.ToInt16(txtCredits.Text), txtClassroom.Text, txtSchedule.Text, int.Parse(txtEnroll.Text), strFacultyID);
        }
        else if (ComboMethod.Text == "Table Update")
        {
            newCourseRow = CSE_DEPTData.Course.NewCourseRow();
            newCourseRow.InsertID = newCourseRow.ID();
            CSE_DEPTData.Course.Rows.Add(newCourseRow);
            insertCount = tableAdapter.Update(CSE_DEPTData.Course);
        }
    }
    else
    {
        intint = tableAdapter.InsertCourse(txtID, txtCourseName.Text,
            Convert.ToInt16(txtCredits.Text), txtClassroom.Text, txtSchedule.Text,
            Convert.ToInt16(txtEnroll.Text), strFacultyID);
    }
    if (int1 == 0)
    {
        ClearCourse();
        cmdInsert.Enabled = false; // clean up all faculty information
    }
    else
    {
        MessageBox.Show("The course insertion is failed");
        cmdInsert.Enabled = true;
    }
    }
}
else
{
    MessageBox.Show("Fill all Course Information box, enter a NULL for any blank column");
}
```

**FIGURE 6.24** The codes for the insert button's click method that will be built, is executed to initialize and

**B.** A user-defined method, **InitCourseInfo()** that will be built, build a **Course[]** array, which is a class-level variable declared in Figure 6.20, to facilitate the pre-checking and post-checking of this data insertion action layer.

**C.** Another user-defined method, **CheckCoursesInfo()** that will be built, is called to check and make sure all TextBoxes in the Course Form have been filled with a valid value to be inserted into the Course table. The result is assigned to the local integer variable check.

**D.** If the result is 0, it means that all TextBoxes have been filled with valid, the data insertion will be performed. The FacultyTableAdapter object, FacultyTableAPT, is cleaned up of any duplicated insert. The reason why we used this FacultyTableAdapter that we need to use one of query methods, **FindFacultyIDByName()** we built in Section 5.12 in Chapter 5 there is no *faculty_name* column available in the Course table, and the only available column is *faculty_id*. Thus we need to get a matched *faculty_id* based on the selected *faculty_name* by the users in this Course Form.