# SQL Server Database Programming with C#

In order to provide a detailed discussion and explanation how to use these two methods to insert records into the database, a real example will be very helpful. Let's first create a Visual Basic project to handle these issues.

# 6.2 INSERT DATA INTO THE SQL SERVER DATABASE USING THE INSERTWARD PROJECT

We have provided a very detailed introduction about the design tools and wizards in Visual Studio. NET in Section 5.1 in the previous chapter, as DataSet, BindingSource, TableAdapter, Data Source window, Data Source configuration and DataSet Designer. We need to use these components to develop our data-inserting project based on the SelectWizard developed in the previous chapter. First let's copy it and carry out some modifications to get our new project. The advantage of creating a new project in this way is that we do not need to redo the data connection and configuration since those have been performed in the previous chapter.

# 6.2.1 Create a New Project Based on the SelectWizard Project

Open the Windows Explorer and create a new folder DB Projects on your local drive. Then browse for the solution SelectWizard Solution, which was developed and built in the previous chapter and located at the folder ClassDB Projects\Chapter 5, which is under the Students folder at the CRC Free tip (refer to Figure 1.2 in Chapter 1). Copy this folder with the project to our new folder DB Projects\Chapter 6.

We can use this as our new project to perform data insertion function to the tables in our sample database.

# 6.2.2 Application User Interfaces

As you know from the last chapter, Form Windows work as the user interfaces for the SelectWizard Project: Login, Selection, Course and Student. All of these five Form Windows contain five buttons: Select, Insert, Delete and Back. We used two buttons, Select and Back in the last chapter, to discuss how to query from our database using that button. In fact, we do not need to build any new Form to perform the data insertion; instead we use the Insert button defined in those Forms to carry out that function. Initially, let' concentrate on the Faculty Form to perform the data insertion into our Faculty table in our sample database.

First, let's concentrate on the data validation before the data can be inserted into the database.

# 6.2.3 Validate Data Before The Data Insertion

The most popular validation is to make sure that date is not empty and it contains a certain value. In other words, we want to make sure that each piece of data has a value, a real value or a NULL value, before they are inserted into the database.

In this application, we validate each piece of faculty information, which is stored in the associated TextBox, is not an empty string unless the user intends to leave it as an empty data. In that case, NULL must be entered. To make this validation simple, we develop a collection and add all of those TextBoxes into that collection. In this way, we don't need to check each TextBox; instead we can use the For Each ...Next loop to scan the collection to find the empty TextBox.