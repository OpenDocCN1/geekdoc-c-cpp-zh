```
73  // validate the data
74  while ( !( validate( data, expression ) ) )
75  {
76      cout << "Invalid " << fieldName << ".\n";
77      cout << "Enter " << fieldName << ": ";
78      getline( cin, data );
79  } // end while
80
81  return data;
82  } // end of function inputData
```

```
Enter last name: Doe
Enter first name: John
Enter address: 123 Some Street
Enter city: Some City
Enter state: Some State
Enter zip code: 12345
Enter phone number: 123-456-7890

Validated Data

Last name: Doe
First name: John
Address: 123 Some Street
City: Some City
State: Some State
Zip code: 12345
Phone number: 123-456-7890
```

Fig. 21.4 | Validating user input with regular expressions. (Part 3 of 3.)

The program first asks the user to input a last name (line 19) by calling the inputData function. The inputData function (lines 65–82) takes two arguments, the name of the data being input and a regular expression that it must match. The function prompts the user (line 70) to input the specified data. Then inputData checks whether the input is in the correct format by calling the validate function (lines 57–62). That function (lines 57–62) takes two arguments—the string to validate and the regular expression it must match. The function first uses the expression to create a regex object (line 60). Then it calls regex_match to determine whether the string matches the expression. If the input isn’t valid, inputData prompts the user to enter the information again. Once the user enters a valid input, the data is returned as a string. The program repeats that process until all the data fields have been validated (lines 19–41). Then we display all the information (lines 44–51).

In the previous example, we searched a string for substrings that matched a regular expression. In this example, we want to ensure that the entire string for each input conforms to a particular regular expression. For example, we want to accept "Smith" as a last name, but not "9@Smith#". We use regex_match here instead of regex_search—regex_match returns true only if the entire string matches the regular expression. Alternatively, you can use a regular expression that begins with a "^" character and ends with a "$" character. The characters "^" and "$" represent the beginning and end of a string,