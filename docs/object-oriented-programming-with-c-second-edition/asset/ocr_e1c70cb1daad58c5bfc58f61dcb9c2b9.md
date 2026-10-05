Listing 7.25 Using the read() function to input strings from disk files

```
/*Beginning of readStringDisk.cpp*/
#include<iostream.h>
#include<fstream>
void main()
{
    ifstream infile("first.dat");
    char cArr[20] = "12345678";
    infile.read(cArr,3);
    cout<<cArr<<endl;
}
/*End of readStringDisk.cpp*/
```

# Output
abc45678

The '3' has been passed as the second parameter to the read() function. It therefore reads only three characters from the file that is associated with the object that has called it.
As know, the name of the array representing the address of the memory block occupied by it. Thus, the first parameter passed to the read() function in the Listing 7.25 is the address of the first byte of the memory block that it occupies. The read() function copies the three characters it has already read into the first three bytes of the array.
A similar method can be devised for using the read() function to read character strings from the keyboard.

5. Extracting objects from input streams using read(): Let us consider the program of Listing 7.19 that was used to output the data of an object into a disk file. The object being output was a simple one, that is, it has no pointers to its data members. The actual data was stored in the file. Suppose the name of the file is first.dat. Listing 7.26 illustrates how the data that was stored in the disk file can be loaded back in an object.

Listing 7.26 Using the read() function to input objects from disk files

```
/*Beginning of readObj.cpp*/
#include<fstream>
class A
{
    /*
    definition of class A
    */
};
void main()
{
    ifstream infile("first.dat");
    A A1;
    infile.read((char *)&A1, sizeof(A));
}
/*/End of readObj.cpp*/
```

Listing 7.26 was simple. Now, let us take the case of complex objects, that objects having embedded pointers.
After reading the section, 'Binary output—the write() function', it is natural to expect that the class of such complex objects will have a suitable function to output the external data structure into disk files. We can also expect the class to have a function that runs