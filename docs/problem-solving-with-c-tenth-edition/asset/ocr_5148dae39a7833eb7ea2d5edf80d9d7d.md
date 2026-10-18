# DISPLAY 16.1 Handling a Special Case Without Exception Handling

```
1   include <iostream>
2   using namespace std;
3
4   int main()
5   {
6       int donuts, milk;
7       double dpg;
8       cout << "Enter number of donuts:\n";
9       cin >> donuts;
10      cout << "Enter number of glasses of milk:\n";
11      cin >> milk;
12
13      if (milk <= 0)
14      {
15          cout << donuts << " donuts, and No Milk!\n" << "Go buy some milk.\n";
16      }
17      else
18      {
19          dpg = donuts/static_cast<double>(milk);
20          cout << donuts << " donuts.\n" << milk << " glasses of milk.\n" << "You have " << dpg << " donuts for each glass of milk.\n";
21      }
22
23      cout << "End of program.\n";
24      return 0;
25  }
```

# Sample Dialogue

```
Enter number of donuts:
12
Enter number of glasses of milk:
0
12 donuts, and No Milk!
Go buy some milk.
End of program.
```

In Display 16.2, we have rewritten the program from Display 16.1 using an exception. This is only a toy example, and you would probably not use an exception in this case. However, it does give us a simple example. Although the program as a whole is not simpler, at least the part between the words try and catch is cleaner, and this hints at the advantage of using exceptions. Look