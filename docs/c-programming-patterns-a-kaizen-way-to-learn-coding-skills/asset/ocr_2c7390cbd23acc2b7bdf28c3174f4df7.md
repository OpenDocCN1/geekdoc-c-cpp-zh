# Strings

It is common programming practice to modify or manipulate text in some way. Some of the examples are dynamically creating web-page url addresses or file paths, extracting specific information from different kinds of file like text files/PDFs/HTML, developing web-scrapping tools that extract text from web-pages. Every programming language provides in-built string libraries for string manipulation. We will experiment with some of commonly used in-built string methods or functions.

# String concatenation

We can output a resultant string by joining one string with another using in-built strcat method or function and this process is known as concatenating strings. The string library to use is;

```
#include <string.h>

char *strcat( char target, const char *source );
```

This method appends source_string to the target string.

# StringConcat.c

```
#include <stdio.h>
#include <string.h>

int main() {
    char name[20] = "Steve" ; // target string
    // appends target string to source string
    strcat( name , " Jobs");
    printf("%s \n", name);
    return 0;
}
```

# Output

Steve Jobs