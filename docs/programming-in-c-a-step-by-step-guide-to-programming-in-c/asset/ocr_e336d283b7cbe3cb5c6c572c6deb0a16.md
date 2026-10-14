If you find that difficulties pervade a program, that the hard parts can't be buried inside black-box functions and then forgotten about; if you find that there are hard parts which involve complicated interactions among multiple functions, then the program probably needs redesigning.

For the purposes of explanation, we've been seeming to talk so far only about “main programs” and the functions they call and the rationale behind moving some piece of code down out of a “main program” into a function. But in reality, there's obviously no need to restrict ourselves to a two-tier scheme. Any function we find ourselves writing will often be appropriately written in terms of sub-functions, sub-sub-functions, etc.

# Program 5.6: Program to create a function that types 65 asterisks in a row

```
```c
/* letterhead1.c */
#include <stdio.h>
#define NAME "MEGATHINK, INC."
#define ADDRESS "10 Megabuck Plaza"
#define PLACE "Megapolis, CA 94904"
#define LIMIT 65
void starbar(void); /* prototype the function */

int main(void)
{
    starbar();
    printf("%s\n", NAME);
    printf("%s\n", ADDRESS);
    printf("%s\n", PLACE);
```
```