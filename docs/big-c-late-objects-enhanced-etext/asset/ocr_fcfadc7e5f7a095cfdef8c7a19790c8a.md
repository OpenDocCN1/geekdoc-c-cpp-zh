+   - **E9.7** Implement a class `StreetAddress`. An address has a house number, a street, an optional apartment number, a city, a state, and a postal code. Supply two constructors: one with an apartment number and one without. Supply a print member function that prints the address with the street (and optional apartment number) on one line and the city, state, and postal code on the next line. Supply a member function `comes_before` that tests whether one address comes before another when the addresses are compared by postal code.

+   - **E9.8** Implement a class `Student`. For the purpose of this exercise, a student has a name and a total quiz score. Supply an appropriate constructor and functions `get_name()`, `add_quiz(int score)`, `get_total_score()`, and `get_average_score()`. To compute the latter, you also need to store the number of quizzes that the student took.

+   - **E9.9** Modify the Student class of Exercise E9.8 to compute grade point averages. Member functions are needed to add a grade and get the current GPA. Specify grades as elements of a class Grade. Supply a constructor that constructs a grade from a string, such as "B+". You will also need a function that translates grades into their numeric values (for example, "B+" becomes 3.3).

+   - **E9.10** Write a class Bug that models a bug moving along a horizontal line. The bug moves either to the right or left. Initially, the bug moves to the right, but it can turn to change its direction. In each move, its position changes by one unit in the current direction. Provide a constructor
+   
+     ```cpp
+     Bug(int initial_position)
+     ```
+   
+     and member functions
+   
+     ```cpp
+     void turn()
+     void move()
+     int get_position()
+     ```
+   
+     Sample usage:
+   
+     ```cpp
+     Bug bugsy(10);
+     bugsy.move(); // Now the position is 11
+     bugsy.turn();
+     bugsy.move(); // Now the position is 10
+     ```
+   
+     Your main function should construct a bug, make it move and turn a few times, and print the actual and expected positions.

+   - **E9.11** Implement a class Moth that models a moth flying along the x-axis. The moth has a position, the distance from a fixed origin. When the moth moves toward a point of light, its new position is halfway between its old position and the position of the light source. Supply a constructor
+   
+     ```cpp
+     Moth(double initial_position)
+     ```
+   
+     and member functions
+   
+     ```cpp
+     void move_to_light(double light_position)
+     double get_position()
+     ```
+   
+     Your main function should construct a moth, move it toward a couple of light sources, and check that the moth’s position is as expected.

+   - **E9.12** Implement classes Person and StreetAddress. Each person has a street address. Provide display functions in each class for displaying their contents. Distribute your code over three source files, one for each class, and one containing the main function. Construct two Person objects and display them.