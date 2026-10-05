# Listing 7.23 Using the read() function to input integer-type value from a disk file

```
*Beginning of readIntDisk.cpp*/
#include<iostream.h>
#include<fstream>
void main()
{
    if (isfile("first.dat")
        int iVar;
        file.read((char*)&iVar,sizeof(iVar));
        cout<<iVar<<endl;
    }
}/*End of readIntDisk.cpp*/
```

# Output
64

As expected, the read() function reads exactly four bytes from the input file that is associated with its invoking object. This is because the value of the second parameter that has been passed to it is It copies the value into the memory address of whose first byte is equal to the first parameter passed to it.

Now, let us look at Listing 7.24 where the read() function is used to read for an integer-type value from the keyboard. By its known characteristics, the read() function is expected to read four bytes from the keyboard, not convert the bytes in any way and copy them into the four bytes that are occupied by the target integer variable.

# Listing 7.24 Using the read() function to input integer-type value from the keyboard

```
*Beginning of readIntConsole.cpp*/
#include<iostream.h>
void main()
{
    int iVar;
    cout<<"Enter a number in base 2 format: ";
    cin.read((char*)&iVar,sizeof(iVar));
    iVar = iVar & 0x000000ff; //Inputting zeros in the upper 3 bytes of the file bytes of iVar*/
    cout<<iVar<<endl;
}/*End of readIntConsole.cpp*/
```

# Output
Enter a number in base 2 format: ABCD<enter>
65

The explanation of this program has been left as an exercise for the reader.

+   3. Extracting floats and doubles from input streams using read() function: Float and double-type values are input in the same way in binary mode as integer-type values.

+   4. Extracting strings from input streams using read() function: Listing 7.25 is a good example for illustrating the use of read() function to read character arrays from a disk file. The contents of a file .dat are as follows:

abcdef