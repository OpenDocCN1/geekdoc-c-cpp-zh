# 4.2 Controlling what happens and in which order

This part is all about if, and then, and else and true and false – the nuts and bolts of how we express and control the execution of a program. This can be very dry and dusty material so to make it more understandable we are going to solve a problem you are going to need to solve to do any interactive web work of any complexity.

We will build something we can use in order to provide something like the functionality that can be obtained from typical getParameter("ITEM1") method in Java servlets or $_REQUEST['ITEM1'] function in PHP.

In Chapter 1 we saw that environment variables can be accessed by the implicit argument to the main function. We can also use the library function getenv() to request the value of any named environment variable.

```
```c
/**********************************************************
 * C Programming in Linux (c) David Haskins 2008
 * chapter4_1.c
 **********************************************************/
#include <stdio.h>
#include <string.h>

int main(int argc, char *argv[], char *env[])
{
    printf("Content-type:text/html\n\n<html><body bgcolor=#23abe2>\n");
    char value[256] = "";
    strncpy(value,(char *) getenv("QUERY_STRING"),255);
    printf("QUERY_STRING : %s<BR>\n", value );
    printf("<form>\n");
    printf("<input type=\"TEXT\" name=\"ITEM1\">\n");
    printf("<input type=\"TEXT\" name=\"ITEM2\">\n");
    printf("<input type=\"SUBMIT\">");
    printf("</form></body></html>\n");
    return 0;
}
```
```

Here we display the QUERY_STRING which is what the program gets as the entire contents of an HTML form which contains NAME=VALUE pairs for all the named form elements.

An HTML form by default uses the GET method which transmits all form data back to the program or page that contains the form unless otherwise specified in an action attribute. This data is contained in the QUERY_STRING as a series of variable = value pairs separated by the & character.