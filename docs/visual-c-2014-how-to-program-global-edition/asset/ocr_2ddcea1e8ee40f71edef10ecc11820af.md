# 7.4 Methods with Multiple Parameters

```
static void Main()
```

but can also be declared by the header:

```
static void Main(string[] args
```

which we'll discuss and demonstrate in Section 8.12, Using Command-Line Arguments. In addition, you can declare Main with return type int (instead of void)—this can be use-ful if an app is executed by another app and needs to return an indication of success or failure to that other app.

# 7.3.4 Additional Comments About Main

Most examples have one class that contained only Main, and some examples had a second class that used Main to create and manipulate objects. Actually, any class can contain a Main method. In fact, each of our two-class examples could have been imple-mented as one class. For example, in the app Figs. 4.11-12, Method Main (lines 7–43 of 4.12) could have been moved into class Account (Fig. 4.11). The app results would have been identical to those of the two-class version. You can place a Main method in every class you declare. Some programmers take advantage of this to build a small test app into classes of your project; however, if you declare more than one method among the classes you declare, you would need to tell the IDE which one you would like to be the app's entry point. To so:

+   1. With the project open in Visual Studio, select Project > [ProjectName] Properties... (where [ProjectName] is the name of your project).
2. Select the class containing the Main method that should be the entry point from the Startup object list box.

# 7.4 Methods with Multiple Parameters

We now consider how to write a method with multiple parameters. Figure 7.3 defines Maximum method that determines and returns the largest of three double values. When the app begins execution, the Main method (lines 8–23) executes. Line 19 calls Maximum (in lines 26–43) to determine and return the largest of these three double arguments. In Section 7.4.3, we'll discuss the use of the + operator in line 22. The sample outputs show Maximum determines the largest value regardless of whether that value is the first, second or third argument.

```
// Fig. 7.3: MaximumFinder.cs
// Method Main with three parameters.
using System;
class MaximumFinder
{
// to float three floating-point values and determine maximum value
static void Main()
}
```

Fig. 7.3 | Method Maximum with three parameters. (Part I of 2.)