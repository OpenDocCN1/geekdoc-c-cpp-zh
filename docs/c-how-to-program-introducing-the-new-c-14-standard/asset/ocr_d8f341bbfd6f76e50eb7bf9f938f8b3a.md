5. 9.7 (*Enhancing Class `Time`*) Modify the `Time` class of Figs. 9.5–9.6 to include a `tick` member function that increments the time stored in a `Time` object by one second. Write a program that tests the `tick` member function in a loop that prints the time in standard format during each iteration of the loop to illustrate that the `tick` member function works correctly. Be sure to test the following cases:

+   A. Incrementing into the next minute.  
+   B. Incrementing into the next hour.  
+   C. Incrementing into the next day (i.e., 11:59:59 PM to 12:00:00 AM).

6. 9.8 (*Enhancing Class `Date`*) Modify the `Date` class of Figs. 9.14–9.15 to perform error checking on the initializer values for data members `month`, `day` and `year`. Also, provide a member function `nextDay` to increment the day by one. Write a program that tests function `nextDay` in a loop that prints the date during each iteration to illustrate that `nextDay` works correctly. Be sure to test the following cases:

+   A. Incrementing into the next month.  
+   B. Incrementing into the next year.

7. 9.9 (*Combining Class `Time` and Class `Date`*) Combine the modified `Time` class of *Exercise 9.7* and the modified `Date` class of *Exercise 9.8* into one class called `DateAndTime`. Modify the `tick` function to call the `nextDay` function if the time