# SQL Database Programming with C#

E. The query FindFacultyByIdByName() that belongs to the FacultyTableAdapter is executed to get a matched faculty_id is reserved to the selected faculty. The retrieved faculty_id is a class-level string variable facultyID for use.

F. If the TableAdapter method is selected, the query InsertCourse() we built in Section 6.3 is used to insert a new course record by picking up six pieces of new information from six TextBoxes in this Form with the queried faculty_id.

G. Alternatively, the TableAdapter Update method is selected, the query InsertRow() we built, newCourseRow, is generated.

H. The generated newCourseRow is inserted into the Table via a user-defined method, InsertRow() which we built. A point is to noted that both the input argument and the returned object look identical, but they are different. The key is that the input argument is a reference object and should be executed first. Therefore the returned object is a running result of this method.

I. The finished newCourseRow cannot be exactly inserted into the Table via the following two methods, Add() and Update().
J. The Store method is selected, the query by a stored procedure InsertCourse() is executed to insert a new course record into the Course Table. One point to noted the data types for columns Credits and Enrollment. The former is a short integer (two bytes) but the latter is a normal integer (four bytes). Therefore, an appropriate conversion method should be used.

K. For any insertion method, if it returns a non-zero value, which means that the insertion is successful and after one row has been inserted into the database, another user-defined method, ClearCourse() we built is called, to cleanup all TextBoxes in this Course Form to enable users to perform some checking and confirming forms for that insertion. In addition, the Insert button is disabled to avoid any possible insertion for the same record.

L. Otherwise, if any insertion method returns a zero, which means that the insertion is failed, a MessageBox with a warning message is displayed to indicate that case, and the Insert button is enabled to allow users to perform next insertion.

M. If the CheckCourseInfo() method returns a non-zero value, which means that some TextBoxes may not be filled with valid values, a MessageBox with a warning message is displayed to indicate that case.

Next's to continue the building of the code for all user-defined methods used in this Insert button's Click method. In total, we have four user-defined methods that need to be coded:

+   * InitCourseInfo()
* CheckCourseInfo()
* InsertCourseRow()
* ClearCourse()

Let's start from the first one, InitCourseInfo().

# 6.3.5 BUILD THE CODES FOR FOUR USER-DEFINED METHODS

The function of the method InitCourseInfo() is to combine all six TextBoxes in the Course Form into a single string or string array CourseInfo[]. With the help of this text, one can access and edit each piece of information stored in a related Table easily.

Open the code window of the Course Form and enter the codes shown in window. All six TextBoxes are assigned to a class-level string array CourseInfo[], which makes it easier to be accessed and modified later.