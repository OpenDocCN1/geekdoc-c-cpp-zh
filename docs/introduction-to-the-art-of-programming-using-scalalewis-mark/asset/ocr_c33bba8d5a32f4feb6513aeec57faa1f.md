modified copies are not efficient, you can make a class using var for each field that needs to change.

Note that by leaving off the case keyword, you do more than just allow for **var** fields. You also lose the copy method, the ability to leave off new when making a new instance of the class, and the ability to do pattern matching. In general, there are many benefits to immutability so you should not take this approach without good reason.

# ### 10.4 Putting it Together

Now we want to use a **case class** along with other things that we have learned to create a small, text-based application. The application that we will write will use the Student that we defined earlier along with the classAverage function and other functions that we will write to make a grade book. This program will be run from a text menu and give us various options similar to what was done in section 8.2.

The program will also use the file handling capabilities that we have learned so that the grades of the students in the course can be saved off and then be loaded back in when we restart the program. The menu for the program will have the following options:

+   1. Add Test Grade
+   2. Add Assignment Grade
+   3. Add Quiz Grade
+   4. Print Averages
+   5. Save and Quit

The program will take a command-line argument for the file to load in. If none is given, the user will be asked how many students are in the section and their names along with the file name to save it under. When one of the first three menu options is selected, the program will list each student's name and ask for their grade. The “Print Averages” option will print out the names of each student along with their grades in each area, their average in that area, and their total average.

There is quite a bit to this program so it is worth breaking it up into different functions and then writing each of those. To do this we can outline what will happen when we run the program and use the outline to break things down then assign function names to things.

+   - **Startup**
+     - load a file (**loadSection**)
+     - or create a section (**createSection**)
+   - **Main menu** (**mainMenu**)
+     - print the menu (**printMenu**)
+     - act on the selection
+       * add a test grade (**addTest**)
+       * add an assignment grade (**addAssignment**)