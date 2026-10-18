+   2. Do Programming Project 3 in Chapter 7. In this version of the problem, return a new dynamic array where all repeated letters are deleted instead of modifying the partially filled array. Don’t forget to free the memory allocated for these returned dynamic arrays when the data is no longer needed.
+   
+   3. Write a function to concatenate the content of two dynamic integer arrays. Your function should contain parameters for two reference pointers to the arrays and the size of both arrays. Your function should return a pointer to a new array which contains a copy of the elements of both arrays. Test your function using a driver program.
+   
+   4. C strings are stored as an array of characters with a special character ‘\\0’ designating the end of the string. Normal *char* arrays are able to function without the special character at the end. Write a function `isCString` which accepts as arguments a const pointer to a char array and an integer for the size of the array. Check along the array for the presence of the special character ‘\\0’. If it exists, return true; otherwise, return false. Write a driver program to test your function by passing C strings, normal char arrays and dynamic char arrays to your function.
+   
+   5. You run four computer labs. Each lab contains computer stations that are numbered as shown in the table below:

| Lab Number | Computer Station Numbers |
|---|---|
| 1 | 1–5 |
| 2 | 1–6 |
| 3 | 1–4 |
| 4 | 1–3 |

Each user has a unique five-digit ID number. Whenever a user logs on, the user’s ID, lab number, and the computer station number are transmitted to your system. For example, if user 49193 logs onto station 2 in lab 3, then your system receives (49193, 2, 3) as input data. Similarly, when a user logs off a station, then your system receives the lab number and computer station number.

Write a computer program that could be used to track, by lab, which user is logged onto which computer. For example, if user 49193 is logged into station 2 in lab 3 and user 99577 is logged into station 1 of lab 4, then your system might display the following:

```
Lab Number  Computer Stations
1           1: empty 2: empty 3: empty 4: empty 5: empty
2           1: empty 2: empty 3: empty 4: empty 5: empty 6: empty
3           1: empty 2: 49193 3: empty 4: empty
4           1: 99577 2: empty 3: empty
```