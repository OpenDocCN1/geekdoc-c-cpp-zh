# # Chapter 4: Array in C++

In any programming language, arrays are crucial. Instead of storing variables or a collection of a similar data type separately, they give a simpler approach of storing them together. The array's values will be accessed one at a time.

So, in this chapter, we will discuss the array completely and understand how to utilize an array in C++ code. The array is a crucial component in C++ since it aids memory management and increases the program's efficiency. Because of its ability to store multidimensional data, it can be employed in a variety of methods. When you need to store the same data type values, an array is always the best option. It not only saves resources but also shortens the time it takes for a program to run.

So, let’s learn how to use an array.

# ## 4.1 Introduction to Array

In C++, an array is a collection of comparable data types such as int, char, float, double, and others that are stored using the index value and can be accessed using simply the index value. It uses a single variable to store all of the instances of variables. In C++, an array can be defined in three ways: by specifying the array's size, directly initializing array elements, or specifying the array's size with its elements.

To allow data to be handled by any application, we must first enter the data into the application. This implies that the value should be saved somewhere in the application until the program executes.

The computer language provides a variable to fulfill the function of storing values. Variables are used to store values so that the application can use them to generate the anticipated result. As values are stored in variables, they take up space in the memory allocated to the application. As a result, the best coding strategy is to ensure that the variable is used as little as feasible. The concept of the array was created to address the memory allocation issue caused by the development of a large number of variables. The array can be thought of as a collection of values of the same datatype.

# ### How do arrays work in C++?

The following is a description of how arrays work:

+   - The array's purpose is to store values of the same datatype. It is designed to work in the same way as the variable, and the only advantage it has over the variable is that it may hold many values at the same time. We must provide the number of variables we wish to store in the array while creating an array in C++ or any other programming language.
+   - It is worth noting that the array's size remains constant during the application's lifetime and cannot be altered dynamically. Once the array's size has been determined, we can store the same number of values in it. If the array's data type is set to an integer, it will not take any values that are not integers. The index will be used to locate the value held by the array.
+   - For example, if the array can hold two values, the second value will be stored at the array's one position because the array's index starts with zero. We will learn how to create arrays in the future.

# ## 4.2 Types of Arrays in C++

Single Dimensional Arrays and Multidimensional Arrays are the two basic forms of variables in the C++ programming language. The single-dimensional array stores values in the form of a list, whereas the multidimensional array stores value in the form of a matrix. We will look at each of the types with an example.

# ### Array with a Single Dimension

A single-dimensional array can be defined as a type of array that can carry the values of a single data center as a list. It is the most basic type of array because it requires little effort to define and initialize. It can be written as inta[10], where int denotes the data type and the array size. The sample below will help to clarify things.