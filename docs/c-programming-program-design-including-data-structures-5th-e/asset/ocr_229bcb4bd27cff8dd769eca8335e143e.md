(initialized to 0 before the while statement) to track how many items have been read. Before executing the body of the while statement, the counter is compared with N. The body of the loop continues to execute until the value of counter is ≥ N. Thus, inside the body of the while statement, the value of counter increases after it reads a new item. In this case, the while loop might look like the following:

```
counter = 0;        //initialize the loop counter variable
while (counter < N) //execute the loop operations
{
    ...
    counter++;
    ...
}
```

If N represents the number of data items in a file, then the value of N can be determined several ways. The program can prompt you to specify the number of items in the file; an input statement can read the value; or you can specify the first item in the file as the number of items in the file, so that you need not remember the number of input values (items). This is useful if someone other than the programmer enters the data.

# EXAMPLE 5.3

Suppose the input is:

8 9 2 3 90 38 56 8 23 98 7 2

Suppose you want to add the numbers and find their average. Consider the following program:

```
#include <iostream>
using namespace std;

int main()
{
    int limit;       //store the number of data items
    int number;      //variable for input
    int sum;         //variable to store the sum
    int counter;     //variable to keep track of items

    cout << "Line 1: Enter the number of "
         << "integers in the list: ";
    cin >> limit;
    cout << endl;
}
```

Numbered Examples illustrate the key concepts with their programming code. The examples are followed by a Sample Run. An explanation then follows that describes what each line in the code does.