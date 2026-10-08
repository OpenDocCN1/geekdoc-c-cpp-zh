| Header File | Library Function | Return Type | Description |
| :--- | :--- | :--- | :--- |
| string.h | strcmpl(str1,str2) | int | Compares two strings lexicographically, ignoring the case of alphabet. It returns 0 if str1 and str2 are identical; a negative value if str1 < str2; and a positive value if str1 > str2. |
| string.h | strcpy(str1,str2) | char* | Copies string str2 into str1. |
| string.h | strlen(str) | int | Returns the number of character in string str. |
| string.h | strset(str,ch) | char* | Sets all character within a string str to ch (excluding the null character \u005c0). |
| time.h | time(ptr) | long int | Returns the number of seconds elapsed beyond a designated base time. |