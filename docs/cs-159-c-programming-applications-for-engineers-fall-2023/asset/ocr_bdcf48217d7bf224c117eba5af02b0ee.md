# **Searching Program #2** - Ask the user to enter a target value and return the location of that value in the array. If the value does not exist,
please inform the user.

```
#define NOTFOUNDERROR -1
#define ARRAYSIZE 15

int binarySearch(int[], int);
int getTarget(void);       //SAME FUNCTION USED IN SEQUENTIAL SEARCH PROGRAM

int main(void)
{
    int array[ARRAYSIZE] = {3, 5, 6, 10, 12, 15, 17, 18, 21, 22, 25, 27, 30, 31, 33};
    int target;            //VALUE WE ARE SEEKING
    int index;             //INDEX VALUE AT WHICH TARGET IS FOUND

    target = getTarget();
    index = binarySearch(array, target);

    if(index == NOTFOUNDERROR)
    {
        printf("Your value %d does not in the array!\n", target);
    }
    else
    {
        printf("Your value %d was found at index %d of the array.\n", target, index);
    }

    return(0);
}
```