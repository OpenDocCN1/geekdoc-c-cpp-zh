```
```java
29     Console.WriteLine($"\nlocal x in method Main is {x}");
30 }
31
32     // create and initialize local variable x during each call
33     static void UseLocalVariable()
34     {
35         int x = 25; // initialized each time UseLocalVariable is called
36
37         Console.WriteLine(
38             $"\nlocal x on entering method UseLocalVariable is {x}");
39         ++x; // modifies this method's local variable x
40         Console.WriteLine(
41             $"local x before exiting method UseLocalVariable is {x}");
42     }
43
44     // modify class Scope's static variable x during each call
45     static void UseStaticVariable()
46     {
47         Console.WriteLine("static variable x on entering method " +
48             $"UseStaticVariable is {x}");
49         x *= 10; // modifies class Scope's static variable x
50         Console.WriteLine("static variable x before exiting " +
51             $"method UseStaticVariable is {x}");
52     }
53 }
54
```
```

```
```text
local x in method Main is 5

local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 1
static variable x before exiting method UseStaticVariable is 10

local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 10
static variable x before exiting method UseStaticVariable is 100

local x in method Main is 5
```
```

Fig. 7.8 | Scope class demonstrates static- and local-variable scopes. (Part 2 of 2.)

Line 8 declares and initializes the static variable x to 1. This static variable is hidden in any block (or method) that declares a local variable named x. Method Main (lines 12–31) declares local variable x (line 14) and initializes it to 5. This local variable's value is output to show that static variable x (whose value is 1) is hidden in method Main. The app declares two other methods—UseLocalVariable (lines 34–43) and UseStaticVariable (lines 46–53)—that each take no arguments and do not return results. Method Main calls each method twice (lines 19–28). Method UseLocalVariable declares local variable x (line 36). When UseLocalVariable is first called (line 19), it creates local variable x and