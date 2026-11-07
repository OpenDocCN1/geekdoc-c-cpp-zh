# # Chapter 2

# # Data Types and Variables

You can think of a computer program as being much like a recipe. What’s in a recipe? A recipe consists of a list of ingredients and a list of instructions for transforming the ingredients into something edible. A computer program consists of data plus instructions that tell the computer how to transform the data into the information wanted from the program. So, to understand how to write programs, we first need to understand how to work with data.

Working with data in C++ involves two things – determining the data types of the data and providing storage space for the data. This chapter will discuss a few of the more common data types in C++ and then explain how to create variables so you can store data in memory while your program is running.

# ## C++ Data Types

Before discussing the various data types used in C++, we need to talk about why having data types is important. First, data types define and limit the range of operations that can be performed on data. For example, it makes sense to add integers together but it doesn’t make sense to add a boolean value to an integer. Along the same line, data types also ensure that the correct type of operation is performed for that type, so that if we want to add two floating-point numbers, the floating-point addition operation will be performed. Otherwise, we would have to have a separate addition operation for each operation rather than being able to use a common operator (+) for all numeric types.

Now let’s look at some of the common data types for C++. They are:

+   1. int – For integer values in the range of approximately
+      -2,000,000,000 to 2,000,000,000