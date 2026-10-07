# 592

# SQL Server Database Programming with C#

![](bbox=[0.188, 0.087, 0.811, 0.473])

**FIGURE 9.79** The running result of the data validation.

user selected and chose course_id from the list box control. The main coding job is performed inside the **SelectedIndexChanged** event of the list box control **CourseList**. When user clicks or selects a **course_id** from the list box control, a **SelectedIndexChanged** event is issued and the event is passed to the selected **SelectedIndexChanged** event to be processed.
To pick up the detailed course information for the selected course_id, the Web method `GetCourse()` in our service project `WebServiceInsertProject` is called. This method returns an instance of the returned class `SQLInsertRecord` to our client project. The detailed course information is stored in that instance.

Double-click on the list box **CourseList** from the Design View of our Course Form **WinForm.cs** from the Solution explorer to expand the **SelectedIndexChanged** event, and the codes that are shown in Figure 9.80 this method. Let's take a closer look at this piece of code to see how it works.

+   A. Two instances, one web service or the proxy class **SQLInsert, SQLResult**, are created here. These instances work as a bridge between our client project and the Web methods developed in the service project.
B. A **Try-Catch** block is used to call the Web method `GetCourse()` with the selected **course_id** from the list box control as the argument to perform this information retrieving. The selected **course_id** is stored in the **Text** property of the **CourseList** control.
C. An exception message is displayed if any error was encountered during the execution of that Web method caught by the system **Catch**.
D. In addition to the error checking performed by the system, we also need to perform our exception checking by inspecting the member data **SQLInsertOK** in the returned class