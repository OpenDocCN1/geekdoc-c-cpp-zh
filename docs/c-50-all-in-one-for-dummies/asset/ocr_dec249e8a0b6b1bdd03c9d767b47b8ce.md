# Chapter 2: Showing Some Class

# In This Chapter

+   ✔ Introducing the C# class
✔ Storing data in an object
✔ Assigning and using object references
✔ Examining classes that contain classes
✔ Identifying static and instance class members
✔ Using constants in C#

You can freely declare and use all the intrinsic data types — such as int, double, and bool — to store the information necessary to make your program the best it can be. For some programs, these simple variables are enough. However, most programs need a way to bundle related data into a neat package.

As shown in Book I, C# provides arrays and other collections for gathering into one structure groups of like-typed variables, such as strings or ints. A hypothetical college, for example, might track its students by using an array. But a student is much more than just a name — how should this type of program represent a student?

Some programs need to bundle pieces of data that logically belong together but aren’t of the same type. A college enrollment application handles students, each with her own name, rank (grade-point average), and serial number. Logically, the student’s name may be a string; the grade-point average, a double; and the serial number, a long. That type of program needs a way to bundle these three different types of variables into a single structure named Student. Fortunately, C# provides a structure known as the class for accommodating groupings of unlike-typed variables.

# Defining a Class and an Object

A class is a bundling of unlike data and functions that logically belong together into one tidy package. C# gives you the freedom to foul up your classes any way you want, but good classes are designed to represent concepts.