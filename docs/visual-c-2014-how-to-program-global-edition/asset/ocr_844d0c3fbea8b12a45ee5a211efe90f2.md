# 304 Chapter 7 Methods: A Deeper Look

```
// UseLocalVariable reinitializes its own local x
UseLocalVariable();

// class Scope's static variable retains its value
UseStaticVariable();

Console.WriteLine($"\nlocal x in method Main is {x}");

// create and initialize local variable during each call
static void UseLocalVariable() {
    int x = 25; // initialized each time UseLocalVariable is called
    Console.WriteLine($"\local x on entering method UseLocalVariable is {x}");
    x++; // modifies this method's local variable
    Console.WriteLine($"\local x before exiting method UseLocalVariable is {x}");
}

// modify Scope's static variable during each call
static void UseStaticVariable() {
    Console.WriteLine($"\nstatic variable on entering method is {x}");
    x = 10; // modifies class Scope's static variable
    Console.WriteLine($"\static variable before exiting is {x}");
}
```

local x in method Main is 5
local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 1
static variable x before exiting method UseStaticVariable is 10

local x on entering method UseLocalVariable is 25
local x before exiting method UseLocalVariable is 26

static variable x on entering method UseStaticVariable is 100
static variable x before exiting method UseStaticVariable is 100

local x in method Main is 5

**Fig. 7.9** Scope class demonstrates static- and local-variable scopes. (Part 2 of 2.)

Line 8 declares and initializes the static variable x to 1. This static variable is hidden in any block (or method) that declares a local variable named x. Method Main (lines 12–31) declares local variable x (line 14) and initializes it to 5. This local variable's value is output to show that static variable x (whose value is 1) is hidden in method Main.