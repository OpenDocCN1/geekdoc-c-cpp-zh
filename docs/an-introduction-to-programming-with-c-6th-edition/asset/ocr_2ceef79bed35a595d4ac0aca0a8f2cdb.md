# The Rearranged Name Program

Figure 13-20 shows the problem specification and IPO chart for the rearranged name program. The program should allow the user to enter a person's first and last names, separated by a space. The program should display the person's last name followed by a comma, a space, and the person's first name. For example, if the user enters "Henry Smith", the program should display "Smith, Henry". As the indicates, you can accomplish this by searching for the space character that separates the first name from the last name. The characters to the left of the space character represent the first name. The characters to the right of the space character represent the last name. You will learn how to search the contents of a string variable in the next section.

Problem specification
Create a program that allows the user to enter a person's first and last names, separated by a space. The program should display the person's last name followed by a comma, a space, and the person's first name. For example, if the user enters "Henry Smith", the program should display "Smith, Henry".

| Input | Processing | Output |
| --- | --- | --- |
| name (first name followed by a space and the last name) | Processing items: space's location | rearranged name (last name followed by a comma, a space, and the first name) |

+   Algorithm:
1. enter the name
2. search the name, looking for the space's location
3. assign the characters to the left of the space's location as the first name
4. assign the characters to the right of the space's location as the last name
5. display the rearranged name, which is the last name followed by a comma, space, and the first name

Figure 13-20 Problem specification and IPO chart for the rearranged name program

# Searching the Contents of a string Variable

You can use the string class' find function to determine whether it contains a specific sequence of characters. For example, you can use the function to determine whether a phone number contains a certain area code. Or, you can use the function to determine whether a street name appears in an address. You can use it to determine the location of the space character that separates a first name from a last name. Figure 13-21 shows the syntax of the find function. In the syntax, string is the name of the string variable you want to search, and searchString is the string for which you are searching. The searchString argument can be a string literal constant or the name of