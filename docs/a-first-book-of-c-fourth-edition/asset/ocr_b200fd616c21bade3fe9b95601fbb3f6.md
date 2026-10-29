5. (Practice) Enter and run Program 14.16.

6. (Debug) Determine why the two unnested try blocks in Program 14.16 cause no problems in compilation or execution. (Hint: Place the declaration for the filename in the first try block and compile the program.)

7. (Debug) a. If the nested try blocks in the preceding Point of Information are separated into unnested blocks, the program won’t compile. Determine why this is so.
b. What additional changes have to be made to the program in Exercise 7a to allow it to be written with unnested blocks? (Hint: See Exercise 6.)

8. (Program) Enter the data for the info.txt file in Figure 14.11 or download it from this book’s Web site (see this book’s introduction for the URL). Then enter and run Program 14.17 and verify that the backup file was written.

9. (Modify) Modify Program 14.17 to use a getline() method in place of the get() method currently in the program.

# 14.5 Input Data Validation

One of the major uses of strings in programs is for user-input validation. Validating user input is essential: Even though a program prompts the user to enter a specific type of data, such as an integer, the prompt doesn’t ensure that the user will comply. What a user enters is, in fact, totally out of the programmer’s control. What is in your control is how you deal with the entered data.

It certainly does no good to tell a frustrated user that “The program clearly tells you to enter an integer, and you entered a date.” Successful programs anticipate invalid data and prevent it from being accepted and processed. Typically, this is accomplished by first validating that input data is of the correct type. If it is, the data is accepted; otherwise, the user is prompted to reenter the data, with an explanation of why the entered data was invalid.

A common method of validating numerical input data is accepting all numbers as strings. Each character in the string can then be checked to make sure it complies with the requested data type. After this check is made and data is verified to be the correct type, the string is converted to an integer or double-precision value by using the conversion functions listed in Table 14.7. (For data accepted with string class objects, the c_str() method must be applied to the string before the conversion function is called.)

As an example, consider inputting an integer number. To be valid, the data entered must adhere to the following conditions:

+   - The data must contain at least one character.
+   - If the first character is a + or - sign, the data must contain at least one digit.
+   - Only digits from 0 to 9 are acceptable following the first character.