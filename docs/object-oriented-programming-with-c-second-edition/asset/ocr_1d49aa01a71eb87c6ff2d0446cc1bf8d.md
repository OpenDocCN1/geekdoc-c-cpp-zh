```
{
  char cArr[20];
  ifstream infile("first.dat");
  infile.getline(cArr,6,'#');
  cout<<cArr<<endl;
}
/End of getlinefile.cpp*/
```

# Output

abcde

If the contents are
abc#def
the output would be 'abc'.
Again, if the contents are

aa bb cc
the output would be 'aa bb'.

# 7.6 Binary Output—write() Function

# 7.6.1 Binary Output—write() Function

The write() function copies the values of variables from memory to the specified output file. It works in binary mode.
As we know, binary functions are not concerned about the data type of the variable that is output. They are only interested in the address of the variable (starting point of the block whose data needs to be output) and the size of the variable (total number of bytes to output). The prototype of the write() function makes this clear:

```
ostream &ostream :: write(const char *, int);
```

The write() function has been defined in the class ostream. It takes two parameters. The first parameter is the address of the variable whose value needs to be output. The second parameter is the size of the variable. The write() function writes the value of the variable to the file that is associated with the object with which it has been called.
Let us now discuss how the write() function is used to output data of various types.

+   1. Inserting characters into output streams using write() function: Listing 7.13 illustrates how the write() function can be used to output the value of a character-type variable to a disk file.

# Listing 7.13 Using the write() function to output character-type value to a disk file

```
/*Beginning of writeCharDisk.cpp*/
#include<fstream.h>
void main() {
  ofstream ofile("first.dat");
  char cVar;
  cVar = 'a';
  ofile.write(cVar,sizeof(char));
}
/*Beginning of writeCharDisk.cpp*/
```