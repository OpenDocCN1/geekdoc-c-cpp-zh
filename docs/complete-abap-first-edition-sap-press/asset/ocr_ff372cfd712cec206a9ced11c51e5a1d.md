![](bbox=[0.148, 0.103, 0.857, 0.461])

**Figure 7-5** START-OF-SELECTION Acts as Default Event

In general, you put all the data selection logic of your ABAP program within the START-OF-SELECTION event. Here, the program starts selecting values from tables. In a typical report program, you initialize the program data under the INITIALIZATION event, validate the selection screen inputs under the selection screen events, and, if everything looks fine, proceed with the data selection (based on the selection criteria) under the START-OF-SELECTION event.

# GET table

The GET table event is used when the executable program uses a logical database for data selection. A logical database is a special ABAP program that retrieves data from the database and makes it available to the application program. In other words, when you use a logical database in your program, you do not need to code the SQL statements to retrieve the data from the database.

The logical database itself contains the Open SQL statements that retrieve the data from the database and pass the data line by line to the interface work area of your application program.