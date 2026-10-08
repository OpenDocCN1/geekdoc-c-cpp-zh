# APPENDIX A

Answers to Mini-Quizzes and Labs

# Mini-Quiz 13-3

+   1. location = cityState.find(",", 0);

+   2. 13

+   3. d. all of the above

# Mini-Quiz 13-4

+   1. d. none of the above

+   2. sentence = sentence + temp.assign(4, '!'););

+   3. b. areaCode = "(\ + areaCode + "");

# Answers to Chapter 13 Labs

![](bbox=[0.311, 0.498, 0.368, 0.573])

# LAB 13-1 Stop and Analyze

+   1. The purpose of the loop is to access each character in the phone variable, one character at a time, in order to remove any parentheses or hyphens.

+   2. The statement in Line 26 assigns the current character from the phone variable to the currentChar variable.

+   3. The selection structure in Lines 27 compares the current character in the phone variable with the opening and closing parentheses. If the current character is an opening parenthesis or a hyphen, the statement in Line 31 removes the current character from the phone variable. The statement in Line 32 subtracts the number 1 from the numChars variable, which keeps track of the number of characters in the phone variable. If the current character is not an opening or closing parenthesis or a hyphen, the statement in Line 35 adds 1 to the count of the subscript variable, which allows to access the next character in the phone variable.

+   4. Before the loop in the program is processed, the statement in Line 21 assigns the number of characters stored in the phone variable to the numChars variable. If the phone variable contains the eight characters 111-2222, the statement assigns the number 8 to the numChars variable. When the statement in Line 31 removes a character from the phone variable, the variable contains one less character. For example, if the statement in Line 31 removes the hyphen from 111-2222 stored in the phone variable, the variable contains seven characters