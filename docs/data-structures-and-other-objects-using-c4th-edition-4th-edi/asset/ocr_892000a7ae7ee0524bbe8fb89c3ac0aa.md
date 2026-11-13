+   17. What is the difference between internal and external iterators?
+   18. Write the insert function for the sequence. Why should this implementation avoid using a copy function from <algorithm>?
+   19. Suppose that a sequence has 24 items, and there is no current item. According to the invariant of the class, what is current_index?
+   20. Suppose g is a sequence with 10 items. You activate g.start(), then activate g.advance() three times. What value is then in g.current_index()?
+   21. What are good boundary values to test the remove_current function?
+   22. Write a demonstration program that asks the user for a list of family member ages, then prints the list in the same order that it was given.
+   23. Write a new member function to remove a specified item from a sequence. The function has one parameter (the item to remove).
+   24. For a sequence of numbers, suppose that you attach 1, then 2, then 3, and so on up to n. What is the big-O time analysis for the combined time of attaching all n numbers? How does the analysis change if you insert n first, then n-1, and so on down to 1—always using insert instead of attach?

# 3.3 INTERACTIVE TEST PROGRAMS

Your sequence class is a good candidate for an interactive test program that follows a standard format. The format, illustrated by the program of Figure 3.10, can be used with any class. The start of the main program declares an object—in this case, a sequence object. The rest of the main program is an interactive loop that continues as long as the user wants. Three things occur inside the loop:

+   1. A small menu of choices is written for the user. Each choice is printed along with a letter or other meaningful character to allow the user to select the choice.
+   2. The user's selection from the menu is read.
+   3. Based on the user's selection, some action is taken on the sequence object.

Our example interactive test program for the sequence is shown in Figure 3.10, with part of a sample dialogue in Figure 3.11 on page 137. Some of the techniques used in the test program are familiar. For example, subtasks, such as printing the menu, are accomplished with functions. Two techniques in the test program may be new to you: converting input to uppercase letters, and acting on the input via a switch statement. We'll discuss these two techniques after you've looked through the program.