# **Program 19.19** A student table (name and score) (Continued)

|  |  |
|---|---|
| George | 71 |
| John | 52 |
| Lucie | 98 |
| Mary | 88 |
| Robert | 77 |

the frequency of words in a string. We use a *map* object named *freq* in which the key is the word encountered in the text and the value is the frequency of words. Note that we have used the ctrl + Z character to signal the end of the input file (Program 19.20).

# **Program 19.20** Frequency of words in text

```
```cpp
1  /*********************************************************
2   * A program to count the number of words in a text        *
3   *********************************************************/
4  #include <map>
5  #include <string>
6  #include <iomanip>
7  #include <iostream>
8  using namespace std;
9
10 int main()
11 {
12   // Declaration of map, iterator, and a string
13   map <string, int > freq;
14   map <string, int > :: iterator iter;
15   string word;
16   // Reading and storing words in the map
17   cout << "Enter a sentence to be parsed: " << endl;
18   while (cin >> word)
19   {
20       ++freq [word];
21   }
22   // Printing the words and their frequency
23   for (iter = freq.begin(); iter != freq.end(); iter++)
24   {
25       cout << left << setw(10) << iter -> first << iter -> second << endl;
26   }
27   return 0;
28 }

Run:
Enter a sentence to be parsed:
we are in the world of this and that and this and that
^Z
```
```