![](bbox=[0.119, 0.12, 0.206, 0.193])

The values and variables that methods act upon are called objects. If you compared Ruby to the English language, think of objects like nouns and methods like verbs.

| Method Name | Description | Example | Result |
|---|---|---|---|
| `.abs` | Returns the absolute value of a number | `-99.abs` | `99` |
| `.round(ndigits)` | Rounds a number to n digits | `3.1415.round(2)` | `3.14` |
| `.floor` | Rounds down to the nearest integer | `4.7.floor` | `4` |
| `.ceil` | Rounds up to the nearest integer | `7.3.ceil` | `8` |

# Using strings and special characters

Along with numbers, variables in Ruby can also store strings. To assign a value to a string use single or double quotation marks.

```
firstname = 'Jack'
lastname = 'Dorsey'
```

To display these variable values, you can puts or print the variable value to the screen. The difference between the two is puts adds a newline (i.e., carriage return) after displaying the value, while print does not.

![](bbox=[0.121, 0.69, 0.205, 0.761])

Variables can also store numbers as strings instead of numbers. Even though the string looks like a number, Ruby will not be able to perform any operations on it. For example, Ruby cannot evaluate this code as is: `amountdue = "18" + 24`.

One issue arises with strings and variables — what if your string itself includes a single or double quote? For example, if I want to store a string with the value “I’m on my way home” or “Carrie said she was leaving for “just a minute””. As is, the double or single quotes within the string would cause problems with variable assignment. The solution is to use special characters called escape sequences to indicate when you want to use characters like quotation marks, which normally signal the beginning or end of a string, or other non-printable characters like tabs. Table 13-3 shows some examples of escape sequences.