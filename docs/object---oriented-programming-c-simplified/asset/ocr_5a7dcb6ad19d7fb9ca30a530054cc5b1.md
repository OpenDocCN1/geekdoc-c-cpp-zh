# EXPLANATION :

The file demo.txt is initially opened in read mode. The function eof returns 0 as long as we are reading from the file. As soon as end of file is reached, function eof returns a non zero value. We read from the file till function eof returns 0. In each iteration of the while loop we read a string str of maximum 99 characters. As soon as end of file is encountered while loop terminates. We close the file and open the append mode by using ios : :app flag. When file is opened in append mode, file pointer is at end of the file. The string is to be appended to the file is taken from user and appended to the file. File is closed again. Next file is opened in read mode and is displayed which shows appended string together with the original contents before appending.

```
/* PROG 12.10 TO READING AND WRITING USING GET AND PUT */

#include <iostream.h>
#include <fstream.h>
#include <stdio.h>
void main()
{
    fstream rw;
    char ch;
    rw.open("temp.txt",ios :: in| ios :: out);
    cout << "Enter some data" << endl;
    cin.get(ch);
    while(ch!=EOF)
    {
        rw.put(ch);
        cin.get(ch);
    }
    rw.seekg(0,ios :: beg);
    while(rw.eof() == 0)
    {
        cout.put(ch);
        rw.get(ch);
    }
    rw.close();
}
```

# OUTPUT :

Enter some data
Hari Mohan Pandey faculty in CSE Dept.(Enter F6 or Ctrl+Z)^Z
Hari Mohan Pandey faculty in CSE Dept.(Enter F6 or Ctrl+Z)

# EXPLANATION :

The two functions put and get allows us to write and read file sequentially. We open the file temp.txt for both reading and writing. We prompt user to enter some data. The data is scanned character by character using get and put into the file one