In the first three sections of this chapter, you review why you would want to sort data, how to use C++ to swap two data values in a program, and how to create a bubble sort in a C++ program. You should do the exercises and labs in this chapter after you have finished Chapter 9 in *Programming Logic and Design, Fifth Edition, Comprehensive*.

# # SORTING DATA

Data records are always stored in some order, but possibly not in the order in which you want to process or view them in your program. When this is the case, you need to give your program the ability to arrange (sort) records in a useful order. For example, the inventory records you need to process might be stored in product-number order, but you might need to produce a report that lists products from lowest cost to highest cost. That means your program needs to sort the records by cost.

Sorting makes searching for records easier and more efficient. Data can be sorted in **ascending order** (lowest to highest for numeric data, or alphabetically for text) or in **descending order** (highest to lowest for numeric data, or reverse alphabetical order for text). People can usually find what they are searching for by simply glancing through a group of data items; but a program must look through a group of data items one by one, making a decision about each one. When searching unsorted records for a particular data value, a program must examine every single record until it either locates the data value or determines that it does not exist. However, when searching sorted records, a program can quickly determine when to stop searching, as shown in the following step-by-step scenario:

+   1. The records used by your program are sorted in ascending order by product number.
+   2. The user is searching for the product number 12367.
+   3. The program locates the record for product number 12368 but has not yet found product number 12367.
+   4. The program determines that the record for product number 12367 does not exist, and therefore stops searching through the list.

Many search algorithms require that data be sorted before it can be searched. (An **algorithm** is a plan for solving a problem.) You can choose from many algorithms for sorting and searching for data. In *Programming Logic and Design, Fifth Edition, Comprehensive*, you learned about three sort algorithms: bubble sort, insertion sort, and selection sort. You also learned about a type of search algorithm: the binary search. Only the bubble sort algorithm is covered in this book.

# # SWAPPING DATA VALUES

Sorting involves swapping data values. When you swap values, you place the value stored in one variable into a second variable, and then you place the value in the second variable in the first variable. You must also create a third variable to temporarily hold one of the values you