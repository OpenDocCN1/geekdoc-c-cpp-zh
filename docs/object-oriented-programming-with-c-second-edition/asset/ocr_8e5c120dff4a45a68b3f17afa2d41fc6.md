# Listing 7.21 Using the read() function to input character-type value from a disk file

```
/*Beginning of readCharDisk.cpp*/
#include<iostream>
#include<fstream>
void main()
{
    ifstream ifile("first.dat");
    char cVar;
    ifile.read(&cVar,sizeof(char));
    cout<<cVar;
}
/*/End of readCharDisk.cpp*/
```

# Output

x

Listing 7.22 illustrates how the read() function can be used to input the value of a character-type variable by making it read from the keyboard.

# Listing 7.22 Using the read() function to input character-type value from the keyboard

```
/*Beginning of readCharConsole.cpp*/
#include<iostream>
void main()
{
    char cVar;
    cout<<"Enter a character: "
    cin.read(&cVar,sizeof(char));
    cout<<cVar;
}
/*/End of readCharConsole.cpp*/
```

# Output

Enter a character: a<enter>

a

It is evident that there is no difference between inputting a character type value in text mode (extraction operator, get() function) and in binary mode (read() function). There is no conversion in either case.

2. Extracting integers from input streams using read() function: Listing 7.23 illustrates how the read() function can be used to input a value into an integer-type variable by making it read from a disk file.

Suppose the first four bytes of a disk file first.dat together contain the binary equivalent of 64.

```
01000000
00000000
00000000
00000000
...
```