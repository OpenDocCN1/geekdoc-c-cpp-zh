# Using decision statements

After completing this chapter, you will be able to:

+   - Declare Boolean variables.
- Use Boolean operators to create expressions whose outcome is either true or false.
- Write if statements to make decisions based on the result of a Boolean expression.
- Write switch statements to make more complex decisions.

Chapter 3, “Writing methods and applying scope,” showed how to group related statements into methods. It also demonstrated how to use parameters to pass information to a method and how to use return to pass information out of a method.

Dividing a program into a set of discrete methods, each designed to perform a specific task or calculation, is a necessary design strategy. Many programs need to solve large and complex problems. Breaking up a program into methods helps you understand these problems and focus on how to solve them, one piece at a time.

The methods in Chapter 3 are very straightforward, with each statement executing sequentially after the previous statement completes. However, to solve many real-world problems, you must also be able to write code that selectively performs different actions and takes different paths through a method depending on the circumstances. In this chapter, you'll learn how to accomplish this task.

# Declaring Boolean variables

In the world of C# programming (unlike the real world), everything is black or white, right or wrong, true or false. For example, if you create an integer variable called x, assign the value 99 to it, and then ask whether x contains the value 99, the answer is definitely true. If you ask if x is less than 10, the answer is definitely