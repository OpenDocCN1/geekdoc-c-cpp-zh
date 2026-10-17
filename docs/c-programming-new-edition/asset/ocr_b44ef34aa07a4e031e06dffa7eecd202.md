In line number 5, as you can see, the character array is initialized to the string in the quotations. The initialized string is entered into an array using the for loop in line number 9. Apart from initializing the i value to 0 the condition in the for loop is set such that the value of i is not equal to 0, i.e., to say the string will be entered into the loop until there are no more characters to be entered and i encounter the null character.

To print the string in the array the printf statement is given which is shown in line number 11. You will also notice here that the format specifier is % C because character array is being entered.

# 7.3. INTERNAL REPRESENTATION OF STRINGS

After your initial stint with strings and having written your first program using strings, it would be reasonable to say that you must be aware of the internal representation of the strings. In this section you will get an overview of how these strings are stored in the memory. The strings representation is no different from that of the integer arrays in the sense that all the characters that constitute the string are stored in contiguous memory locations. That is to say the first character will be stored in the 0th position and the second in the 1st and so on.

The last character as you know is the null character. You will now see how the string is stored in the memory.

B O N D \0 1234 1235 1236 1237 1238

As you can see the string bond is stored in a sequential manner and each character occupies one byte each but the point to observe here is that the string is terminated with a null character.

Another word about the length of the string is that if the length of a string is predefined, i.e., the number of spaces in the memory to be reserved for the particular string, then the null character is placed immediately after the last character and the rest of the spaces reserved are left empty. E.g., if the string is declared as char str[10]= “bond”; The representation of the above string would be in the following fashion.

![](bbox=[0.22, 0.94, 0.82, 1.0])

B O N D \0. As you can see after the null character the rest of the spaces are lying empty and this is not a healthy sign for the programmer.