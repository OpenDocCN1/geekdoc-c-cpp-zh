+   - Finally, underflow is overridden as follows:
+     - First underflow determines the number of characters that could potentially be ungot. If that number of characters are ungot, the input buffer is exhausted. So this value may be any value between 0 (the initial state) or the input buffer's size (when the reserved area has been filled up completely, and all current characters in the remaining section of the buffer have also been read);
+     - Next the number of bytes to move into the reserved area is computed. This number is at most d_reserved, but it is set equal to the actual number of characters that can be ungot if this value is smaller;
+     - Now that the number of characters to move into the reserved area is known, this number of characters is moved from the input buffer's end to the area immediately before d_base;
+     - Then the buffer is refilled. This all is standard, but notice that reading starts from d_base and not from d_buffer;
+     - Finally, streambuf's read buffer pointers are set up. Eback is set to move locations before d_base, thus defining the guaranteed unget-area, gptr is set to d_base, since that's the location of the first read character after a refill, and egptr is set just beyond the location of the last character read into the buffer.

Here is underflow's implementation:

```
```cpp
int FdUnget::underflow()
{
    size_t ungetsize = gptr() - eback();
    size_t move = std::min(ungetsize, d_reserved);

    memcpy(d_base - move, egptr() - move, move);

    int nread = read(d_fd, d_base, d_bufsize);
    if (nread <= 0)        // none read -> return EOF
        return EOF;

    setg(d_base - move, d_base, d_base + nread);

    return *gptr();
}
```
```

# An example using FdUnget

The next example program illustrates the use of the class FdUnget. It reads at most 10 characters from the standard input, stopping at EOF. A guaranteed unget-buffer of 2 characters is defined in a buffer holding 3 characters. Just before reading a character, the program tries to unget at most 6 characters. This is, of course, not possible; but the program nicely ungets as many characters as possible, considering the actual number of characters read:

```
```cpp
#include "fdunget.h"
#include <string>
#include <iostream>
#include <istream>
using namespace std;

int main()
{
    FdUnget fds(0, 3, 2);
    istream is(&fds);
    char   c;

    for (int idx = 0; idx < 10; ++idx)
```
```