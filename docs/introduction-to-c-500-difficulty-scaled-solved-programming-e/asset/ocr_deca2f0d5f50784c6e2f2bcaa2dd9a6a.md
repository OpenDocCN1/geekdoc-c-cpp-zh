```
if(str1 == str2)
{
  cout << "The same line is: " << str1 << '\n';
  found = 1;
  break; /* Since a common line is found, exit from the
loop. */
}
if(found == 0)
{
  cout << "There is no common line\n";
  fin_f.close();
  fin_s.close();
  return 0;
}
```

C.24.5 Write a program that reads the name of a file and displays its second line. There is a restriction to use get() and not getline().

```
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main()
{
  int ch, lines;
  string fname;

  cout << "Enter file name: ";
  cin >> fname;
  ifstream fin(fname.c_str());
  if(fin.is_open() == false)
  {
    cout << "Error: is_open() failed\n";
    exit(EXIT_FAILURE);
  }
  cout << "Line contents: ";
  lines = 1;
  while(1)
  {
    ch = fin.get();
    if(!fin) || (lines > 2))
      break;
    if(lines == 2) /* Only the characters of the second line are displayed displayed. */
      cout << (char)ch;
      if(ch == '\n') /* Once the new line character is read, increment
the lines++;
  }
  fin.close();
  return 0;
}}
```

Comments: Once the program displays the second line, the loop terminates.