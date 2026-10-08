```
/*
/* main: Input and Store Strings
/* **********************************************************************************/
/* Input Variables:
/* name[NUM] [STRLNG] - list of names
/* Output Variables:
/* name[NUM] [STRLNG] - list of names
/*
/* Functions Called:
/* funcinput() - function to input names
/* funcoutput() - function to output names
/* **********************************************************************************/

#include <stdio.h>
#include <string.h>

#define NUM 10
#define STRLNG 40

void funcinput(char [][STRLNG]);
void funcoutput(char [][STRLNG]);

int main()
{
    char name[NUM] [STRLNG];

    funcinput(name);
    funcoutput(name);

    return 0;
}
*************************************************************************************************/
/*
/* funcinput - Input Strings
/*
*************************************************************************************************/
/*
/* Input Parameters:
/* strname[NUM][STRLNG] - array storage
/*
/* Output Parameters: - list of names
/* name[NUM] [STRLNG] */
```