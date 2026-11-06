```
```cpp
}
/*
    Generated output on file argv[1]

    at cin.get();

Several messages to stderr, msg 1
Several messages to stderr, msg 2

    at the end of the program:

Several messages to stderr, msg 1
Several messages to stderr, msg 2
Several messages to stderr, msg 3
*/
```
```

+   - At lines 1-2 local variables are defined: `errlog` is the `ostream` to write the error messages too, and `cerr_buffer` is a pointer to a `streambuf`, to point to the original `cerr` buffer.
+   - At line 3 the alternate error stream is opened.
+   - At line 4 redirection takes place: `cerr` now writes to the `streambuf` defined by `errlog`. It is important that the original buffer used by `cerr` is saved, as explained below.
+   - At line 5 we pause. At this point, two lines were written to the alternate error file. We get a chance to take a look at its contents: there were indeed two lines written to the file.
+   - At line 6 the redirection is terminated. This is very important, as the `errlog` object is destroyed at the end of `main`. If `cerr`'s buffer would not have been restored, then at that point `cerr` would refer to a non-existing `streambuf` object, which might produce unexpected results. It is the responsibility of the programmer to make sure that an original `streambuf` is saved before redirection, and is restored when the redirection ends.
+   - Finally, at line 7, `Done` is again written to the screen, as the redirection has been terminated.

# ### 6.6.2 Reading AND Writing streams

In order to both read and write to a stream an `std::fstream` object must be created. As with `ifstream` and `ofstream` objects, its constructor receives the name of the file to be opened:

```
```cpp
fstream inout("iofile", ios::in | ios::out);
```
```

Note the use of the constants `ios::in` and `ios::out`, indicating that the file must be opened for both reading and writing. Multiple mode indicators may be used, concatenated by the bitor operator. Alternatively, instead of `ios::out`, `ios::app` could have been used and mere writing would become appending (at the end of the file).

Reading and writing to the same file is always a bit awkward: what to do when the file may not yet exist, but if it already exists it should not be rewritten? Having fought with this problem for some time I now use the following approach:

```
```cpp
#include <fstream>
#include <iostream>
#include <string>

using namespace std;

int main()
```
```