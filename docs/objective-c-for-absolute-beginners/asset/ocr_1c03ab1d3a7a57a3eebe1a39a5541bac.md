![](bbox=[0.137, 0.093, 0.762, 0.439])

**Figure 4-10.** Project options for RandomNumber

Now, you need to open the implementation file in the Source group. This is where you will write your Objective-C code.

+   3. Open the main.m file. Delete the following line of code:
4. You are ready to write your app. Start writing the code under

NSLog("Hello, World!");
// insert code here..

See Figure 4-11.

```
```
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    autoreleasepool {
        // insert code here...
        NSLog("Hello, World!");
    }
    return 0;
}
```
```

**Figure 4-11.** The editor is now ready for you to write your code.

Following your Alice code, you will write your random number generator app. You will notice that most of the code is very similar to your Alice app. See Listing 4–9.