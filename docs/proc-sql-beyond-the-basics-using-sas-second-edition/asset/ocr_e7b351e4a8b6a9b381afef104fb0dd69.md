# Chapter 9: Troubleshooting and Debugging

+   Introduction ........................................................................................ 323
+   The World of Bugs................................................................................ 324
+   The Debugging Process ........................................................................ 324
+   Types of Problems ................................................................................ 326
+   Troubleshooting and Debugging Techniques ........................................ 327
+     Validating Queries with the VALIDATE Statement................................ 327
+     Documented PROC SQL Options and Statement................................... 328
+   Undocumented PROC SQL Options ....................................................... 342
+     Macro Variables ................................................................................ 343
+     Troubleshooting and Debugging Examples.......................................... 345
+   Summary ................................................................................................ 350

# Introduction

When it comes to tracking down the source of SQL coding problems, users can be very resourceful. To find all those pesky errors, warnings, notes, and unexpected results, you need to carefully inspect the SAS log and telltale clues from code reviews and sample runs. Using reliable troubleshooting and debugging techniques will help get to the root of any syntax, data, system-related, and logic errors that are or could be problematic to the successful execution of a PROC SQL program.

This chapter introduces a number of strategies and techniques for troubleshooting and debugging SQL procedure coding problems. The guidelines presented in this chapter will help you learn about the different types of bugs, the steps involved in troubleshooting problems, the types of errors that can occur, and the options and statements that are available in the SQL procedure to troubleshoot and debug problems.