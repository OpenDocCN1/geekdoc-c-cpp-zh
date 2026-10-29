# Display 2.11 Program to Read the Text File in Display 2.10

```
1 #include <iostream>
2 #include <fstream>
3 #include <string>
4 
5 using namespace std;
6 int main( )
7 {
8     string firstName, lastName;
9     int score;
10    fstream inputStream;
11 
12    inputStream.open("player.txt");
13 
14    inputStream >> score;
15    inputStream >> firstName >> lastName;
16 
17    cout << "Name: " << firstName << " "
18    << lastName << endl;
19    cout << "Score: " << score << endl;
20    inputStream.close();
21 
22    return 0;
23 }
```

# Sample Dialogue

```
Name: Gordon Freeman
Score: 100510
```

Often you will want to know if the program has read everything in a file. One way to do this is to note that the stream extraction operator returns true if the read was successful and false if it was not. So if we attempt to read past the end of the file then >> will return false and we can ignore the result. This may look a bit strange because on one line we are both performing a read action and checking a Boolean result. Display 2.12 uses a while loop to read every line of data from the player.txt file as a string and outputs it.

# Display 2.12 Using a Loop to Read the Text File in Display 2.10 (part 1 of 2)

```
1 #include <iostream>
2 #include <fstream>
3 #include <string>
4 
5 using namespace std;
6 int main( )
```