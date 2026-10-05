# CHAPTER 9 Strings

Display 9.3 Some Functions in &lt;ctype&gt; (part 1 of 2)

| FUNCTION | DESCRIPTION | EXAMPLE |
| --- | --- | --- |
| toupper (Char_Exp) | Returns the uppercase version of Char_Exp (as a value of int). | `char c = toupper('a');`
cout << c;`
Outputs: A` |
| tolower (Char_Exp) | Returns the lowercase version of Char_Exp (as a value of int). | `char c = tolower('A');`
cout << c;`
Outputs: a` |
| isupper (Char_Exp) | Returns true provided Char_Exp is an uppercase letter, otherwise returns false. | `if (isupper(c))`
cout << "Is uppercase.";
else
cout << "Is not uppercase.";` |
| islower (Char_Exp) | Returns true provided Char_Exp is a lowercase letter, otherwise returns false. | `char c = 'a';`
if (islower(c))
cout << "a is lowercase.";
Outputs: a is lowercase.` |
| isalpha (Char_Exp) | Returns true provided Char_Exp is a letter of the alphabet; otherwise, returns false. | `char c = '$';`
if (isalpha(c))
cout << "Is a letter.";
else
cout << "Is not a letter.";
Outputs: Is not a letter.` |
| isdigit (Char_Exp) | Returns true if Char_Exp is one of the digits '0' through '9'; otherwise, returns false. | `if (isdigit('3'))`
cout << "It's a digit.";
else
cout << "It's not a digit.";
Outputs: It's a digit.` |
| isnum (Char_Exp) | Returns true if Char_Exp is either a letter or a digit; otherwise, returns false. | `if (isalnum('3') && isnum('a'))`
cout << "Both alphanumeric.";
else
cout << "One or more are not.";
Outputs: Both alphanumeric.` |
| isspace (Char_Exp) | Returns true provided Char_Exp is a whitespace character, such as the blank or newline character; otherwise, returns false. | `//Skips over one "word" and sets c
//equal to the first whitespace
//character after the word":
do {
cin.get(c);
}
while (!isspace(c));` |
| ispunct (Char_Exp) | Returns true provided Char_Exp is a printing character other than whitespace, a digit or a letter; otherwise, returns false. | `if (ispunct('?'))`
cout << "Is punctuation.";
else
cout << "Not punctuation.";` |