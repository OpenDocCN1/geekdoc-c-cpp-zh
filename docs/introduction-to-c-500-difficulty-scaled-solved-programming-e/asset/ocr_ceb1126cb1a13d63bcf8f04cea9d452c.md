# 402 Introduction to C++

U.13.11 Define the structure type Car with members: model, price, and manufacture year. Write a program that uses this type to read the data of 100 cars and store them in an array. Then, the program should provide a menu to perform the following operations:

+   1. Show model. The program should read a model and display the related information, if registered. If the user enters *, the program should show the information of all models.
2. Show prices. The program should read a price and show all models that cost more.
3. Program termination.

U.13.12 Define the structure Any_Type with an integer member (e.g., s_type) and a member of type union. The union's members are a structure of type Time (e.g., t) as defined in U.13.7 and a structure of type Student (e. g, s) as defined in U.13.6. Write a program that reads integers and stores it into the s_type member of a variable of Any_Type. Then, the program should check the value of s_type and read data according to that value. If it is 1 the input data should be stored into the t member, otherwise it should be stored into the s member.

U.13.13 Define the union Selected_Type with the members named: u_char (of type char), u_int (of type int), u_float (of type float), and u_double (of type double). Define the structure Var_Type with the members named: type (of type int) and st (union of Selected_Type). Write a function that takes as parameter a structure of Var_Type. The function should read a number according to the value of the type member, store that number in the appropriate st member, and display the value of the type. Write a program that prompts the user to enter a number that represents the data type (i.c., 1: char, 2: int, 3: float, 4: double) and then uses the function to read a corresponding value and display it.