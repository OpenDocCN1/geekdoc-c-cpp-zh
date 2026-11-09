# # LET'S MAKE A SUBSTITUTION

Visual Basic provides the **Replace method** for replacing a sequence of characters in a string with another sequence of characters, such as replacing area code “(800)” with area code “(877)” in a phone number. Figure 24-4 shows the syntax of the Replace method and includes examples of using the method. In the syntax, *oldValue* is the sequence of characters that you want to replace in the *string*, and *newValue* is the replacement characters. When processing the Replace method, the computer makes a temporary copy of the *string* in memory, and then replaces the characters in the copy only. The Replace method returns a string with *all* occurrences of *oldValue* replaced with *newValue*.

**USING THE REPLACE METHOD**

| Syntax | Purpose |
|---|---|
| `string.Replace(oldValue, newValue)` | replaces every occurrence of *oldValue* with *newValue* |

**Example 1**

```vb
strPhone = "(800) 111-2222"
strPhone = strPhone.Replace("(800)", "(877)")
```

assigns the string "(877) 111-2222" to the strPhone variable

**Example 2**

```vb
strWord = "latter"
strWord = strWord.Replace("t", "d")
```

assigns the string "ladder" to the strWord variable

Figure 24-4: Syntax and examples of the Replace method

# # I NEED TO FIT THIS IN SOMEWHERE

Rather than replacing characters in a string, an application may need to insert characters in a string. You insert characters using the **Insert method**. Possible uses for the method include inserting an employee’s middle initial within his or her name, or inserting parentheses around the area code in a phone number. Figure 24-5 shows the Insert method’s syntax.