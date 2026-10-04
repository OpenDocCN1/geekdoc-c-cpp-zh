# Appendix D

# 813

![](bbox=[0.19, 0.09, 0.831, 0.365])

argv[0]=3280388
argv[1]=3280395
argv[2]=3280401
argv[3]=3280407

**Figure D.5** The command line stored in memory

# Program D.2

```
// A program that displays its command-line arguments
#include <iostream>
using namespace std;

int main(int argc, char *argv[])
{
    int i;

    cout << "\nThe following arguments were passed to main():\ ";

    for (i = 0; i < argc; i++)
        cout << argv[i] << " " ";

    cout << endl;

    return 0;
}
```

Assuming the executable version of Program D.2 is named PGMD-2.exe, the output for the command line C:\>PGMD-2 three blind mice is the following:

The following arguments were passed to main(): PGMD-2 three blind mice