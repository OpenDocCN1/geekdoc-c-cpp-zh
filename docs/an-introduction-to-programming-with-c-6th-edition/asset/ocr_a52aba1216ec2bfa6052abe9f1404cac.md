# CHAPTER 14 Sequential Access Files

(continued)

| Output | |
| --- | --- |
| CD name | string cdName = ""; |
| artist name | string artistName = ""; |

Algorithm

+   1. open the cds.txt file for input
2. if (the.txt file was opened successfully)
   read the CD name and artist name from the cds.txt file

```
inFile.open("cds.txt", ios::in);
if (inFile.is_open()) {
  getline(inFile, cdName, '#');
  getline(inFile, artistName);
  while (inFile.eof()) {
    cout << cdName << " - " << artistName << endl;
    getline(inFile, cdName, '#');
    getline(inFile, artistName);
  }
  inFile.close();
} else {
  cout << "File could not be opened." << endl;
}
```

else
display the "File could not be opened." message
end if

Figure 14-11 pop information chart and C++ instructions for the CD collection program

Figure 14-12 shows the entire CD collection program, with the instructions pertaining to sequential access files shared. Figure 14-13 shows a sample run of the program, and Figure 14-14 shows the cds.txt file opened in a text editor.

```
// CD Collection.cpp - keeps track of a CD collection
//Created/revised by <your name> on <current date>
#include <iostream>
#include <string>
#include <fstream>
using namespace std;
//function prototypes
void saveCds();
void displayCds();
int main() {
  int menuOption = 0;
```

Figure 14-12 CD collection program (continues)