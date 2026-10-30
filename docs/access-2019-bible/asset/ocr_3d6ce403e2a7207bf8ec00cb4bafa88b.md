For example, Right("Microsoft", 4) would return four characters starting from the rightmost character (soft).

The Mid function returns a specified number of characters starting from a specified character position. The required arguments for the Mid function are the text you're evaluating, the starting position, and the number of characters you want returned. For example, Mid("Lonely", 2, 3) would return three characters, starting from the second character, or character number two in the string (one).

> Tip
> In a Mid function, if there are fewer characters in the text being used than the length argument, the entire text will be returned. For example, Mid("go", 1, 10000) will return go. As you'll see later in this chapter, this behavior comes in handy when you're working with nested functions.

Figure 11.24 demonstrates how the MyTest field was updated to the correctly formatted phone number.

Take a moment to analyze the query breakdown:

+   - "(": This text will add an open parenthesis to the resulting string.
+   - &: The ampersand is a character operator that joins strings together.
+   - Left([Phone],3): This function will extract the left 3 characters of the [Phone] field.
+   - &: The ampersand is a character operator that joins strings together.
+   - ")": This text will add a close parenthesis to the resulting string.
+   - &: The ampersand is a character operator that joins strings together.
+   - Mid([Phone],4,3): This function will extract the three characters of the [Phone] field starting from character number four.
+   - &: The ampersand is a character operator that joins strings together.
+   - "-": This text will add a dash to the resulting string.
+   - &: The ampersand is a character operator that joins strings together.
+   - Right([Phone],4): This function will extract the right four characters of the [Phone] field.

# Padding Strings to a Specific Number of Characters

You may encounter a situation where key fields are required to be a certain number of characters in order for your data to be able to interface with peripheral platforms such as ADP payroll systems or SAP databases.

For example, imagine that the CompanyNumber field must be ten characters long. Those that are not ten characters long must be padded with enough leading zeros to create a ten-character string.