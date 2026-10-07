
# Storage Duration, Scope, and Linkage

variable called dick. The static modifier makes this variable local to the file and over-rides the global definition. Then the file defines an external variable called harry. It can do without conflicting with the harry of the first file because the first harry has internal linkage. Then the remote_access() displays the addresses of these three variables so that you can compare them with the addresses of the corresponding variables in the first file. Remember that you need to compile both files and link them to get the complete program.

# Listing 9.7 twofile1.cpp

```cpp
//twofile1.cpp -- variables with external and internal linkage
#include <iostream>    // to be compiled with file2.cpp
int tom = 3;               // external variable definition
int dick = 30;             // external variable definition
static int harry = 300;   // static, internal linkage

// function prototype
void remote_access();

int main()
{
    using namespace std;
    cout << "main()" reports the following addresses:\n"; 
    cout << &tom << " = &tom, " << &dick << " = &dick, " ";
    cout << &harry << " = &harry\n";
    remote_access();
    return 0;
}
```

# Listing 9.8 twofile2.cpp

```cpp
//twofile2.cpp -- variables with internal and external linkage
#include <iostream>
extern int tom;           // tom defined elsewhere
static int dick = 10;      // overrides external dick
int harry = 200;          // external variable definition,
                             // no conflict with twofile harry

void remote_access()
{
    using namespace std;
    cout << "remote_access()" reports the following addresses:\n";
    cout << &tom << " = &tom, " << &dick << " = &dick, " ";
    cout << &harry << " = &harry\n";
}
```

# Chapter 9 Memory Models and Namespaces

Here is the output from the program produced by compiling Listings 9.7 and 9.8 together:

```
main() reports the following addresses:
0x0041a020 = &tom, 0x0041a024 = &dick, 0x0041a028 = &harry
remote_access() reports the following addresses:
0x0041a020 = &tom, 0x0041a050 = &dick, 0x0041a054 = &harry
```

As you can see, the tom both use the same tom variable but different dick and harry variables. (The particular address values and formatting may be different on your system, the tom both will match each other, and the dick and harry addresses won't.)

# Static Storage Duration, No Linkage

So far, we've looked at a file-scope variable with external linkage and a file-scope variable with internal linkage. Now let's look at the third member of the static duration family: local variables with no linkage. You create such a variable by applying the static modifier to a variable defined inside a block. When you use it inside a block, static causes a local variable to have static storage duration. This means that though the variable is known within that block, it exists even while the block is inactive. Thus a local variable can preserve its value between function calls. (Static variables would be useful for reincarnation you could use them to pass secret account numbers for a Swiss bank to your appearance.) Also if you initialize a static variable, the program initializes the variable once, when the program starts up. Subsequent calls to the function don't reinitialize the variable the way they do for automatic variables. Listing 9.9 illustrates these points.

# Listing 9.9 static.cpp

```cpp
//cpp -- using a static local variable
#include <iostream>
// constants
const int ArSize = 10;

// function prototype
void strcount(const char * str);

int main()
{
  using namespace std;
  char input[ArSize];
  char next;

  cout << "Enter a line: \n";
  cin.get(input, ArSize);
  while (cin)
  {
    cin.get(next);
    while (next != '\n') // string didn't fit!
      cin.get(next); // dispose of remainder
    strcount(input);
    cout << "Enter next line (empty line to quit):\n";
    if (!cin.get(input, ArSize))
      break;
  }

  cout << "Bye\n";
  return 0;
}

void strcount(const char * str)
{
  using namespace std;
  static int total = 0; // static local variable
  int count = 0; // automatic local variable
  cout << "\"" << str << "\" contains \n";
  while (*str++) // go to end of string
    count++;
  total += count;
  cout << count << " characters\n";
  cout << total << " characters total\n";
}
```

Incidentally, the program in Lining 9.9 shows one way to deal with line input that may exceed the size of the destination array. Recall that the cin.get(input, ArSize) input method returns up to the end of the line or up to ArSize - 1 characters, whichever comes first. It leaves the newline character in the input queue. This program uses cin.get(next) to read the character that follows. If next is a newline character, then the preceding call to cin.get(input, ArSize) must have read the whole line. If next isn't a newline character, there are more characters left on the line. This program then uses a loop to reject the rest of the line, but you can use the fact that attempting to read an empty line with get(char *, int) causes cin to test as false.
Here is the output of the program in Lining 9.9:

Enter the line:
nice pants

"nice pant" contains 9 characters
9 characters total
Enter next line (empty line to quit):

thanks
"thanks" contains 6 characters
15 characters total

Enter next line (empty line to quit):
parting is such sweet sorrow
"parting i" contains 9 characters
24 characters total

Enter next line (empty line to quit):
ok
"ok" contains 2 characters
26 characters total

Enter next line (empty line to quit):

By

# Chapter 9 Memory Models and Namespaces

# Storage Duration, Scope, and Linkage

Additional information about storage classes:

```cpp
auto
static
extern
``` 

This book doesn't use volatile or mutable, but there is more to learn about const.

# More about const

In C++ (but not C), the const modifier alters the default storage classes slightly. Whereas a global variable has external linkage by default, a const global variable has internal linkage by default. That is, C++ treats a global const definition, such as in the following code fragment, as if the static specifier had used:

```cpp
const int fingers = 10; // same as static int fingers = 10;
int main(void)
{
  ...
}
```

# Cv-Qualifiers

Certain keywords, called storage specifiers, provide additional information about storage. Here's a list of storage specifiers:

```cpp
auto (added in C++11)
static
extern
thread_local (added in C++11)
register (deprecated in C++11)
mutable (added in C++11)
```

# Cv-Qualifiers

Here are the cv-qualifiers:

```cpp
const
volatile
```

(As you have guessed, v stands for const and volatile.) The most commonly used-qualifier is const, and you've already seen its purpose: We will come back to const in a moment.

The volatile keyword indicates that the value in a memory location can be altered though nothing in the program modifies it. This is less mysterious than it sounds. For example, you could have a pointer to a hardware location that contains the time or a port. In this case, the hardware, not the program, changes the contents. The intent of this keyword is to improve the optimization abilities of compilers. For example, suppose the compiler notices a program uses the value of a particular variable twice within a few statements. Rather having the program look up the value twice, the compiler might cache the value in a register. This optimization ensures that the value does not change between the two uses. If you don't declare a variable volatile, the compiler can feel free to make this optimization. If you do declare a variable volatile, you're telling the compiler not to make that sort of optimization.

# mutable

Now let's return to mutable. You can use it to indicate that a particular member of a structure (or class) can be altered even if a particular structure (or class) variable is const. For example, consider the following:

```cpp
struct data
{
  char name[30];
  mutable int accesses;
  ...
}
const data veep = {"Claybourne Clodde, 0, ... };
strcpy(veep.name, "Joye Joux"); // not allowed
veep.accesses++; // allowed
```

The const qualifier veep prevents a program from changing veep's members, but the mutable qualifier to access member shields from that restriction.
