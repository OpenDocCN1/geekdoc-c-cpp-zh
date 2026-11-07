|  |  |
|---|---|
| **3. Repeat (counter < size or !success)**<br>    a. read next item<br>    b. success = criteria<br>    c. counter++<br>**4. if success**<br>    a. write success message<br>**5. else**<br>    a. write failure message | **3. Repeat (counter < size or success)**<br>    a. read next item<br>    b. success = criteria<br>    c. counter++<br>**4. if success**<br>    a. write success message<br>**5. else**<br>    a. write failure message |

# Write the Program

Since the two programs are very similar, we give the code for the case of *any* and leave the case of *all* as an exercise. Program 5.22 shows the code. We have a validation loop, a search loop, and a post-loop decision to check if the item meeting the given criterion was found or not.

**Program 5.22**   Finding if *any* item in a list meets a given criterion

```
```cpp
/************************************************************
 * The program search a list of item to find if any item is  *
 * divisible by 7.                                         *
 ************************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Declaration
    bool success;
    int size;
    int item;
    // Input Validation
    do
    {
        cout << "Enter the number of items in the list: ";
        cin >> size;
    } while (size < 0);
    // Processing
    for (int i = 0; (i < size) && (!success); i++)
    {
        cout << "Enter the next item: ";
        cin >> item;
        success = (item % 7 == 0);
    }
    // Checking success or failure
```
```