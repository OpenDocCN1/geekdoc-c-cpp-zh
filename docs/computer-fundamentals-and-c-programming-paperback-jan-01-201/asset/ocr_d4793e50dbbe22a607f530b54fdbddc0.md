# ### 9.10.3 Handling String Data (%s)

We know a string as an array of characters terminated by NUL (5.15), but that is not how scanf understands a string. To scanf, a string is simply a token or word, i.e. a set of one or more non-whitespace characters. scanf reads this word with the %s format specifier and the name of the array as its matching argument. Thus, if you have defined an array named stg as

```
```c
char stg[20];  // Array must be of type char
```
```

then you can fill up the array by using scanf like this:

```
```c
scanf("%s", stg);  // stg not &stg
```
```

scanf ignores leading whitespace and reads until it encounters a whitespace character or EOF. It saves the word in the array stg and tags a NUL character at the end. This means that the array must have an extra element for NUL. Note that scanf doesn't use the & prefix when %s is used. The name of the array itself provides the address that scanf needs.

The word-based approach used by scanf makes it unsuitable for reading a multi-word string. To match three words, scanf needs three %s specifiers (a single one for printf) and the addresses of three arrays. There are two solutions to this problem and one of them is discussed in Section 9.11.1.

> > **Takeaway:** printf and scanf differ in their treatment of %s. This specifier matches a single word in scanf but one or more words in printf.

# ### 9.10.4 scanf_char_string.c: Characters and Strings as Input

Program 9.7 uses %c and %s to handle character and string input. It also uses the field width to split a string into three. The getchar sequence is used twice to clear the buffer, so it makes sense to use a macro (FLUSH_BUFFER) in this program.

Because whitespace in the control string ("%c %c %c") matches zero or more occurrences of leading whitespace in the data, we could key in both ABC and a b c. The final invocation of scanf uses "%3s%3s%3s" to split the string septenov into three separate strings. Each array has an extra byte to let scanf append the NUL at the end.

# ## 9.11 scanf: OTHER FEATURES

Our coverage of the scanf function would not be complete without a discussion on the (i) the scan set, (ii) the only flag supported by it, and (iii) some more format specifiers. These topics are examined in the following sections.

# ### 9.11.1 The Scan Set Specifier

The scan set specifier comprises one or more characters enclosed by [ and ]. For instance, %[aeiou] represents a scan set that matches only vowel characters. However, a caret at the beginning of the