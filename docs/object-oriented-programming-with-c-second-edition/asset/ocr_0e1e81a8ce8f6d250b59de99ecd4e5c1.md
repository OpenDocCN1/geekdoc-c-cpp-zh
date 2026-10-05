# Object-Oriented Programming with C++

```
cout<<"File does not exist for reading\n";
/*
  statements to take corrective action
*/
```

Another reason can be that the file is being opened for writing using the ios::noreplace flag but it already exists.

```
ofstream ofile;
ofile.open("first.dat", ios::out | ios::noreplace);
if(ofile.fail()) {
  cout<<"File already exists ... overwrite (y/n)";
  /*
    statements to record user's response and take
    appropriate action
  */
}
```

Some more reasons that cause the read/write operation to fail:

+   - The file being opened for writing is read only.
- There is no space on the disk.
- The file being opened for writing is in a disk that is write-protected.

# 7.12.3 bad() Function

bad() function returns true whenever a function that is reading from a file encounters a serious I/O error. Under such circumstances, the value of the badbit flag gets set to true. It is to abort I/O operations on the stream in this situation.

# 7.12.4 clear() Function

clear() function is used to clear the bits returned by the bad() function. This is necessary under a number of circumstances. Listing 7.28 illustrates one circumstance.

**Listing 7.28** *clearEof() function*

```
/*Beginning of clearEOF.cpp*/
#include<iostream>
#include<fstream>
void main() {
  fstream ofile("first.dat",ios::in | ios::out);
  char cArr[100];
  int i=0;
  while(ofile.eof()) {
    ofile.get(cArr[i++]);
    ofile.clear();
    for(int j=0;j<i; j++)
      ofile.put(cArr[j]); //append the contents of the
// file to itself
  }
}
/*End of clearEOF.cpp*/
```