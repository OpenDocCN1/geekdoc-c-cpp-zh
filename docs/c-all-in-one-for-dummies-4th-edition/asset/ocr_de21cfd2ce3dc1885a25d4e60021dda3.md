therefore, they can’t steal the password for use with the target application. Other examples of hash use are to:

+   - Verify a file’s hash to a previously saved hash value to ensure no one has modified the file.
+   - Compare two files to ensure they’re most likely the same.
+   - Make dictionary searches fast.

Code::Blocks provides excellent support for hashes. However, in order to use it, you must enable support for C++11 extensions using the technique found in the “Working with ranges” section of Book 1, Chapter 5. After you enable the required support, you can create the HashingStrings example shown here to demonstrate the use of hashes.

```
```cpp
#include <iostream>
#include <unordered_map>

using namespace std;

int main() {
  hash<const char*> MyHash;
  cout << "The hash of \"Hello World\" is:" << endl;
  cout << MyHash("Hello World") << endl;
  cout << "while the hash of \"Goodbye Cruel World\" is:"
       << endl;
  cout << MyHash("Goodbye Cruel World") << endl;
  return 0;
}
```
```

The example begins by creating a hash function object, MyHash. You use this function object to convert input text to a hash value. The function object works just like any other function, so you might provide the input text as MyHash("Hello World"). Hashes always output precisely the same value given a particular input. Consequently, you should see the following output from this example.

```
```text
The hash of "Hello World" is:
4952133
while the hash of "Goodbye Cruel World" is:
4952192
```
```