Display 13.22 shows a simple program that illustrates how the queue class is used. This program reads a word one letter at a time and places the letters in a queue. The program then removes the letters one by one and writes them to the screen. Because data is removed from a queue in the order in which it enters the queue, the output shows the letters in the word in the same order that the user entered them. It is good to contrast this application of a queue with a similar application using a stack that we gave in Display 13.18.

# DISPLAY 13.22 Program Using the Queue Class (part 1 of 2)

```
1  //Program to demonstrate use of the Queue class.
2  #include <iostream>
3  #include "queue.h"
4  using namespace std;
5  using namespace queuesavitch;
6  
7  int main()
8  {
9      Queue q;
10     char next, ans;
11 
12     do
13     {
14         cout << "Enter a word: ";
15         cin.get(next);
16         while (next != '\n')
17         {
18             q.add(next);
19             cin.get(next);
20         }
21 
22         cout << "You entered: ";
23         while ( ! q.empty() )
24             cout << q.remove();
25         cout << endl;
26 
27         cout << "Again?(y/n): ";
28         cin >> ans;
29         cin.ignore(10000, '\n');
30     } while (ans !='n' && ans != 'N');
31 
32     return 0;
33  }
```

> <The ignore member of cin is discussed in Chapter 8. It discards input remaining on the current input line up to 10,000 characters or until a return is entered. It also discards the return ('\n') at the end of the line.>