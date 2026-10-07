# Reading a Character

![](bbox=[0.158, 0.115, 0.768, 0.442])

Figure 12-5: The input buffer after cin >> courseNum followed by cin.getline(name,80)

Since the newline character remains in the input buffer, you do not have the opportunity to enter input into the next statement: the call of the getline member function. Instead, Figure-12-5 depicts, the getline member function, which removes whitespaces as well as newline character from the input buffer and assigns newline character to the character array name. While the character array name has assigned value, it is not a printable character, so it appears in the output that name has no value.

The solution, pointed out in the previous section, is to follow use of the cin object and the stream extraction operator (>>) with the no-argument of the ignore (or get) member function. However, unlike with the stream extraction operator (>>) always leaves a newline character in the input buffer. The following modification of the previous program implements this solution by adding a call to the no-argument version of the ignore member function after use of the cin object with the stream extraction operator (>>):

```
#include <iostream>
using namespace std;

int main(void)
{
    char name[80];
    int courseNum;
    cout << "Enter course number: ";
    cin >> courseNum;
    cin.ignore();
    cout << "Enter your name: ";
    cin.getline(name, 80);
    cout << "Course: " << courseNum << endl;
```