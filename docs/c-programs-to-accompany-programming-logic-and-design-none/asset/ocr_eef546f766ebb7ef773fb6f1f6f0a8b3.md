Execute this program using the following input values:

+   - Monday – 3 hours (employee 1)
+   - Tuesday – 4 hours (employee 1)
+   - Wednesday – 5 hours (employee 1)
+   - Thursday – 5 hours (employee 1)
+   - Friday – 3 hours (employee 1), 4 hours (employee 2)
+   - Saturday – 7 hours (employee 1), 8 hours (employee 2)
+   - Sunday – 0 hours

The program results should include:

+   - A total of 3 hours worked on Monday.
+   - A total of 4 hours worked on Tuesday.
+   - A total of 5 hours worked on Wednesday.
+   - A total of 5 hours worked on Thursday.
+   - A total of 7 hours worked on Friday.
+   - A total of 15 hours worked on Saturday.
+   - A total of 0 hours worked on Sunday.
+   - A grand total of 39 hours worked for the week.

# # MULTIPLE-LEVEL CONTROL BREAK PROGRAMS

In Chapter 8 of *Programming Logic and Design, Fifth Edition*, you learned how to implement a multiple-level control break program. Make sure you understand this material before you continue with this chapter.

A multiple-level control break program performs special processing in response to more than one condition. In this section, you will study a modified version of the Bookstore program, which makes use of a multiple-level control break. In this version, the program generates a report that prints a summary of books sold in each city and each state. To generate this type of summary report, a control break must occur when the name of the city changes. A second control break must occur when the name of the state changes.

You learned that for a single-level control break program, the input must be sorted according to a predetermined control break variable; similarly, the input for a multiple-level control break program must be sorted by multiple control break variables. In this case, the input must be sorted by city within state.