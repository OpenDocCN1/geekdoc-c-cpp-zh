# Table 15.2 C-String Library Functions (Require the Header File cstring) (continued)

| Name | Description | Example |
|---|---|---|
| strcmp(stringExp1,stringExp2) | Compares stringExp1 with stringExp2. Returns a negative integer if stringExp1 < stringExp2, 0 if stringExp1 == stringExp2, and a positive integer if stringExp1 > stringExp2. | strcmp("Bebop","Beehive") |
| strncpy(stringVar,stringExp,n) | Copies at most n characters of stringExp to stringVar. If stringExp has fewer than n characters, it pads stringVar with "0"s. | strncpy(str1, str2, 5) |
| strncmp(stringExp1,stringExp2, n) | Compares at most n characters of stringExp1 with stringExp2. Returns the same values as strcmp() based on the number of characters compared. | strncmp("Bebop","Beehive",2) |
| strchr(stringExp, character) | Locates the first occurrence of the character in the string. Returns the address of the character. | strchr("Hello", 'l') |
| strtok(string1, character) | Parses string1 into tokens. Returns the next sequence of characters contained in string1, up to but not including the delimiter character character. | strtok("Hello there World!",',') |

The first four functions listed in Table 15.2 are used most often. The strcpy() function copies a source C-string expression, which consists of a string literal or the contents of a C-string variable, into a destination C-string variable. For example, in the function call strcpy(string1, "Hello World!"), the source string literal "Hello World!" is copied into the destination C-string variable string1. Similarly, if the source string is a C-string variable named src_string, the function call strcpy(string1, src_string) copies the contents of src_string into string1. In both cases, it's the programmer's responsibility to ensure that string1 is large enough to contain the source C-string (see the previous Point of Information).

The strcat() function appends a string expression to the end of a C-string variable. For example, if the contents of a C-string variable named dest_string is "Hello", the function call strcat(dest_string, " there World!") results in assigning the string value