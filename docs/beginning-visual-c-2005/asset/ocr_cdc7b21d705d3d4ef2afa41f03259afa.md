# Chapter 8

definition, your code will not compile. You’ve seen this code already, so I won’t discuss it again. It would be a good idea to save the file at this point by clicking the Save toolbar button. Get into the habit of saving the file you’re editing before you switch to something else. If you need to edit the constructor again, you can get to it easily by either double-clicking its entry in the lower pane on the Class View tab or by selecting it from the right drop-down menu above the pane displaying the code.

You can also get to a member function’s definition in a .cpp file or to its declaration in a .h file directly by right-clicking its name in the Class View pane and selecting the appropriate item from the context menu that appears.

# Adding Function Members

You need to add all the functions you saw earlier to the CBox class. Previously, you defined several function members within the class definition, so that these functions were automatically inline. You can achieve the same result by entering the code in the class definition for these functions manually, or you can use the Add Member Function wizard.

You might think that you can define each inline function in the .cpp file, and add the keyword inline to the function definitions, but the problem here is that inline functions end up not being “real” functions. Because the code from the body of each function has to be inserted directly at the position it is called, the definitions of the functions need to be available when the file containing calls to the functions is compiled. If they’re not, you’ll get linker errors and your program will not run. If you want member functions to be inline, you must include the function definitions in the .h file for the class. They can be defined either within the class definition, or immediately following it in the .h file. You should put any global inline functions you need into a .h file and #include that file into any .cpp file that uses them.

To add the GetHeight() function as inline, right-click on CBox on the Class View tab and select Add > Add Function from the context menu. You then can enter the data defining the function in the dialog that is displayed, as Figure 8-11 shows.

![](bbox=[0.175, 0.57, 0.765, 0.905])

Figure 8-11