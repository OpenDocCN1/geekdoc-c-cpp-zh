In Program 4, we have defined two functions, namely, main and findmax. The function main accepts the array elements and passes it to the function findmax. The function findmax accepts an address of array and returns an integer value. We observed the use of int *temp in the function findmax, where temp represents the pointer that can store address of integer variable. As the array defined in function main was of integer type, the pointer temp accepted the address of the first element of the array and then itself started working as an array. All the values were obtained by using the aforementioned address formula.

Let us take one more example to see the working of a single-dimensional array. Program 5 sorts the numbers entered in descending order of values:

# ► Program 5

```
/* Program to sort an array */

#include <stdio.h>
#define MAX 5
/* Function sort */
void sort(int *temp)
{
    int i_temp,i_ictlr,i_jctr;

    for(i_ictlr = 0; i_ictlr < MAX-1; i_ictlr++)
    for(i_jctr = i_ictlr + 1; i_jctr < MAX; i_jctr++)
    {
        if(temp[i_ictlr] <= temp[i_jctr])
        {
            i_temp = temp[i_ictlr];
            temp[i_ictlr] = temp[i_jctr];
            temp[i_jctr] = i_temp;
        }
    }
}
/* End of function sort */

/* Beginning of main function */
main()
{
    /* Declare variables */
    int i_ctr;
    int i_array[MAX];

    /* Read Data */
    for(i_ctr = 0; i_ctr < MAX; i_ctr++)
    {
        printf("\nElement %d: ",i_ctr + 1);
        scanf("%d",&i_array[i_ctr]);
    }

    /* Function Call */
    sort(i_array);

    /* Print Data */
    printf("Sorted Array\n");
    for(i_ctr = 0; i_ctr < MAX; i_ctr++)
```