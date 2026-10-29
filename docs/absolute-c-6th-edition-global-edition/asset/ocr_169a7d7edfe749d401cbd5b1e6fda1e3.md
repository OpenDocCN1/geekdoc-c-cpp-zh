# Display 18.6 Function Returning a High Score without Exceptions (part 1 of 2)

```
1 // Program that outputs the high score from a high scores file.
2 // Does not use exception handling.
3 #include <iostream>
4 #include <fstream>
5 #include <string>
6 using std::cout;
7 using std::endl;
8 using std::ifstream;

9 //Function prototypes
10 int getHighscore();

11 // Returns the high score in the scores.txt file.
12 int getHighscore()
13 {
14     ifstream f;
15     int high = -1;
16     f.open("scores.txt");
17     // Check if the file did not open
18     if (f.fail())
19     {
20         cout << "File could not be opened." << endl;
21         return -1;
22     }
23     int num;
24     // Scan through each number in the file and return the largest.
25     f >> high;
26     while (f >> num)
27     {
28         if (num > high)
29             high = num;
30     }
31     f.close();
32     return high;
33 }

34 int main()
35 {
36     int highscore = getHighscore();
37     cout << "The high score is " << highscore << endl;
38     return 0;
39 }
```