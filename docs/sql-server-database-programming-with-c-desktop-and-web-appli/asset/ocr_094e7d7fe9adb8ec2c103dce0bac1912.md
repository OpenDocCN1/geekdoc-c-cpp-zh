3. Using the tools and wizards provided by Visual Studio.NET and ADO.NET to perform the data updating for the Student table via the Student Form in the SelectWizardProject (the project file is located at a folder DB Projects\Chapter 7\SelectWizard Solution under the Students folder at the CRC Press fpt site (refer to Figure 1.2 in Chapter 1).

**Hint1:** The binding to all TextBoxes in the Student Form to all columns in the Student table in our sample database has been done and related components have been generated.

**Hint2:** Build the query function UpdateStudent(), with Data Designer.

**Hint3:** Develop code in the Student.cs code window, exactly inside the Update button's Click method, to call the query function to perform this data updating.

4. Using the Runtime objects to complete the data query for the Student Form to the Student by using the project RTUpdateDelete (the project file is located at the folder, DB Projects\Chapter 7\UpdateRequestDelete located under the Students folder at the CRC Press fpt site (refer to Figure 1.2 in Chapter 1).

5. Using the stored procedure to complete the data-updating query for the Course Form to the Course by using the project SPUpdateDeleteProject (the project file is located at the folder: DB Projects\Chapter 7\SPUpdateDeleteSolution located under the Students folder at the CRC Press fpt site (refer to Figure 1.2 in Chapter 1).

**Hint:** One can choose to use the codes in Exercise 2 with the built stored procedure dbo.UpdateCourse in exercise.

6. Using the LINQ to SQL to complete the data-deleting query for the Student Form to the Student by using the project LINQSelectProject (the project file is located at the folder: DB Projects\Chapter 7\LINQSelect Solution under the Students folder at the CRC Press fpt site (refer to Figure 1.2 in Chapter 1).

**Hint1:** It is highly recommended to delete new inserted student member to avoid the complicated data recovery process. A good way is to run any exercise projects, such as exercise 3, 4, or 5, in the Homework of Chapter 6, to insert a new student member with the following information (then delete this new inserted record):

| Student ID | 83658 |
| Student Name | Susan Bai |
| GPA: | 3.88 |
| Credits: | 96 |
| Major | Computer Science |
| SchoolYear:| Junior |
| Email: | sbai@college.edu |
| image: | White.jpg |

**Hint2:** Four tables are involved in this data deleting: Student, Login, Course and StudentCourse if an original student record were deleted. The recovery order is: first, recover the record from the parent table (Student table), and then recover all records for all other child tables.