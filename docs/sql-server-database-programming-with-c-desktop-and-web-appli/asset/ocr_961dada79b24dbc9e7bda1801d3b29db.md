# Data Inserting with Visual C#.NET

this new created DataRow. The codes and the function of this user-defined method are explained later. The method returns a completed DataRow that contains all the pieces of information about the new record. One point to be noted is that it is a reference parameter, ref newlyRow, is passed into the method, which means the address (not the value) of the object newlyRow is passed into the method, and any modification to it is permanent. We need this permanent property to keep our returned newlyRow updated.

D. The completed DataRow is added to the Faculty in our DataSet. One point to be noted is that adding a new record into a data table in the DataSet is nothing to do with adding a new record into a data table. The data tables are only mappings of real data tables in the database. To add this we need to perform the next step.

E. The TableAdapter's method Update() is executed to make this record added into the real database. As mentioned before, you can control the amount of data to be added into the database by passing different arguments. Here we want to add one new record into the Faculty, so a data table is the argument. This Update() returns an integer value to indicate whether this update is successful or not. The value of the returned integer is the number of rows that have been successfully added into the database. A returned value of zero means that this update is failed since no new row has been added into the database.

Now let's develop the codes for the user-defined method InsertFacultyRow(). Open the Window of the Faculty Form and enter the codes that are shown in Figure 6.15 into that window for this method. The function of this code is straightforward and easily understood. First a local byte array, blmage, is generated and the user-defined method, getCurrentImage(), is called to get the selected Faculty image is inserted. Seven pieces of new information stored in the selected TextBoxes with the selected image are added into the new DataRow object, exactly added into a new row of the faculty table in the DataSet. Since the facultyRow is passed into this method using a reference value, any modification to it means that this modification can be returned to the calling method and kept valid until the project is terminated or exited.

At this point, we have completed the coding development for our data insertion using the use of two methods. Now let's test our coding by running the project. Click on the Start button to run the project. Enter the username and password to the Login Form, and select the Faculty Information from the Selection window to open the Faculty Form window, which is shown in Figure 6.15.

| SelectWizardProject | InsertFacultyRow() |
| --- | --- |
| private void InsertFacultyRow(ref CSE_DEPTDataSet.FacultyRow facultyRow) |
| {
    byte[] blmage;
    blmage = getCurrentImage();
    facultyRow.id = txtFacultyID.Text;
    facultyRow.name = txtFacultyName.Text;
    facultyRow.title = txtTitle.Text;
    facultyRow.office = txtOffice.Text;
    facultyRow.phone = txtPhone.Text;
    facultyRow.college = txtCollege.Text;
    facultyRow.email = txtEmail.Text;
    facultyRow.image = blmage;
}|

FIGURE 6.15 The codes for the user-defined method InsertFacultyRow().