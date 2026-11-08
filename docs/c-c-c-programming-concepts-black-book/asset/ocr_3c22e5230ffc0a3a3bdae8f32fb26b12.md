# The if-else Statement

Now, we will demonstrate another program, which will contain if-else statement. We will slightly modify the preceding program to behave as follows:

```
```cpp
1:// Demonstrating "if-else" statement in C++
2:#include <iostream>
3:using namespace std;
4:int main ()
5:{
6:    int num;
7:    cout<<"Enter a number: ";
8:    cin >> num;
9:    if (num % 2) {
10:        cout<<"You have entered an odd number"<<endl;
11:    } else {
12:        cout<<"You have entered an even number"<<endl;
13:    }
14:    return 0;
15:}
```
```

In the preceding program, we are giving a user an opportunity to enter a number, checking it, and then displaying whether it is an odd number or an even number. Following is the output of the preceding program:

```
```
Output from the First Run:
    Enter a number: 11
    You have entered an odd number

Output from the Second Run:
    Enter a number: 44
    You have entered an even number
```
```

Now, let’s see an example of nested if-else statement by combining the last two programs into one with nested if checks. Initially we check for positive or negative number, and if the entered number is positive, then we check for even or odd number, as follows:

```
```cpp
1:// Demonstrating "nested if-else" statement in C++
2:#include <iostream>
3:using namespace std;
4:
5:int main ()
6:{
7:    int num;
8:    cout<<"Enter a number: ";
9:    cin >> num;
10:        if (num > 0) {
11:            if (num % 2) {
12:                cout<<"You have entered an odd number"<<endl;
13:            } else {
14:                cout<<"You have entered an even number"<<endl;
15:            }
16:        }
17:        else {
18:            cout<<"You have entered a negative number"<<endl;
19:        }
20:        return 0;
21:}
```
```