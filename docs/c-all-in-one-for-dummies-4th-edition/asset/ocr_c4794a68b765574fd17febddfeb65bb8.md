![](bbox=[0.163, 0.094, 0.226, 0.16])

It would be nice to create an entire directory-tree structure in one fell swoop — doing a call such as `mkdir("/abc/def/ghi/jkl")` without having any of the `abc`, `def`, or `ghi` directories already existing — but each parent directory must exist before you attempt to create a child directory. The function won’t create a `jkl` directory unless the `/abc/def/ghi` directory exists. That means you have to break this call into multiple calls: First create `/abc`. Then create `/abc/def`, and so on.

![](bbox=[0.163, 0.22, 0.226, 0.286])

If you do want to make all the directories simultaneously, you can use the `system()` function, as described in “Using the quick-and-dirty method” section, later in this chapter. If you execute `system("mkdir \\abc\\def\\ghi\\jkl")`, you can make the directory in one fell swoop.

# Deleting a directory

To delete a directory, you call the `rmdir()` function, passing the name of the directory. If you want to find out whether it worked, test its results against 0. Here’s some sample code as found in the DeleteDirectory example:

```
```cpp
#include <iostream>
#include <stdio.h>
#include <io.h>

using namespace std;

int main() {
  if (rmdir("./abc") != 0)
    cout << "Directory not deleted." << endl;
  else
    cout << "Directory deleted." << endl;

  return 0;
}
```
```

After you run this example, the `/CPP_A104/BookVI/Chapter04/abc` directory that you created in the previous section goes away. Make sure you verify that the directory is added and removed as expected. If you run this example a second time, you see the “Directory not deleted.” message because you can’t delete a directory that doesn’t exist.

![](bbox=[0.163, 0.802, 0.226, 0.867])

This approach works only if the directory is empty. If the directory has at least one file or directory in it, the function can’t remove the directory — and returns a nonzero result.