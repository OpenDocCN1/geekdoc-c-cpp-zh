The include directive that goes at the top of your file is

```
#include <fstream>
```

Your code also needs the following:

```
using namespace std;
```

+   2. fin.open("stuff1.dat");
+   if (fin.fail())
+   {
+       cout << "Input file opening failed.\n";
+       exit(1);
+   }
+   fout.open("stuff2.dat");
+   if (fout.fail())
+   {
+       cout << "Output file opening failed.\n";
+       exit(1);
+   }

+   3. fin.close();
+   fout.close();

+   4. You need to replace the stream outStream with the stream cout. Note that you do not need to declare cout, you do not need to call open with cout, and you do not need to close cout.

+   5. #include <cstdlib>
+   
+   Your code also needs the following:
+   using namespace std;

+   6. The exit(1) function returns the argument to the operating system. By convention, the operating system uses a 1 as an indication of error status and 0 as an indication of success. What is actually done is system-dependent.

+   7. bla.dobedo(7);

+   8. Both files and program variables store values and can have values retrieved from them. Program variables exist only while the program runs, whereas files may exist before a program is run and may continue to exist after a program stops. In short, files may be permanent; variables are not. Files provide the ability to store large quantities of data, whereas program variables do not provide quite so large a store.

+   9. We have seen the open, close, and fail member functions at this point. The following illustrate their use.