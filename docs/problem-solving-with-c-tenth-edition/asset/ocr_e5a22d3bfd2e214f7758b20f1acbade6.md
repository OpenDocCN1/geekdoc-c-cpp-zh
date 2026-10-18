# PITFALL  Confusing the Global Namespace and the Unnamed Namespace

Do not confuse the global namespace with the unnamed namespace. If you do not put a name definition in a namespace grouping, then it is in the global namespace. To put a name definition in the unnamed namespace, you must put it in a namespace grouping that starts as follows, without a name:

```
namespace
{

```

Both names in the global namespace and names in the unnamed namespace may be accessed without a qualifier. However, names in the global namespace have global scope (all the program files), while names in an unnamed namespace are local to a compilation unit.

This confusion between the global namespace and the unnamed namespace does not arise very much in writing code, since there is a tendency to think of names in the global namespace as being “in no namespace,” even though that is not technically correct. However, the confusion can easily arise when discussing code.

# SELF-TEST EXERCISES

+   12. Would the program in Display 12.8 behave any differently if you replaced the *using* directive
+   
+   ```cpp
+   using namespace dtimesavitch;
+   ```
+   
+   with the following *using* declaration?
+   
+   ```cpp
+   using dtimesavitch::DigitalTime;
+   ```

+   13. What is the output produced by the following program?
+   
+   ```cpp
+   #include <iostream>
+   using namespace std;
+   
+   namespace sally
+   {
+       void message( );
+   }
+   namespace
+   {
+       void message( );
+   }
+   int main( )
+   {
+       {
+           message( );
+   ```