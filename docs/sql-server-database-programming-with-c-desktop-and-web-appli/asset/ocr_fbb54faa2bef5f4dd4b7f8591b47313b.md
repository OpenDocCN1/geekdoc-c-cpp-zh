# III. EXERCISES

+   1. Write a paragraph to answer and explain the following questions:
   a. What is ASP.NET?
   b. What is the main component of the ASP.Net Web application?
   c. How is an ASP.Net Web application executed?

+   2. Suppose we want to delete one record from the Student table in our sample database CSE_DEPT based on one student_id='H10201'. List all deleting steps and deleting queries including the data deleting the child and the parent tables.

+   3. Figure 8.10 shows a piece of codes developed in the Page_Load() method. Explain the functionality of the statement if (IsPostBack) block.

| Course | Page_Load() |
|---|---|
 protected Page_Load(object sender, EventArgs args)
 {
 if ((OracleConnection)Application["oraConnection"]).State != ConnectionState.Open
 { ((OracleConnection)Application["oraConnection"]).Open();
 if (IsPostBack)
 {
 ComboName.Items.Add("Ying Ball");
 ComboName.Items.Add("Davis Balla");
 ComboName.Items.Add("Black Anderson");
 ComboName.Items.Add("Steve Johnson");
 ComboName.Items.Add("Kenney King");
 ComboName.Items.Add("Alice Brown");
 ComboName.Items.Add("Debby Angles");
 ComboName.Items.Add("Lef Henry");
 }
 }
 |

**FIGURE 8.10** The codes for the Page_Load method.

+   4. Use page Course.aspx and develop codes to the Delete button's Click method to delete a course record in the SQLWebUpdateDelete Project, which can be found from the folder Class DB Projects' Chapter 8 that is located on the CRC Press ftp site (refer to Figure 1.2 in Chapter 1). Reference Section 8.8 to insert first a new course CSE-668 by running WebLoginSQL Course Project, and test this deleting action since course CSE-668 is a new course without any relationship with other tables.

+   5. Use the page Course.aspx and develop codes to the Update button's Click method to update a course record in that SQLWebUpdateDelete Project, which can be found from the folder Class DB Projects Chapter 8 that is located on the CRC Press ftp site (refer to Figure w in Chapter 1). It is highly recommended that you restore the updated course back to the original one.

+   6. Use the page Student.aspx and develop the codes to call two stored procedures, dbo.StudentInfo and dbo.StudentCourse, built into the previous projects, to select one record from the Student table by using the project SQLWebSelectProject (the project can be found from the folder Class DB Projects\Chapter 8 that is located on the CRC Press ftp site (refer to Figure 1.2 in Chapter 1)). Use the Select button's Click method to perform this query action.