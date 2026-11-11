Java's `import` documents the dependencies of the package in which it appears on the packages named in the `import`. These dependencies are less obvious when `import` is not used.

# ### 11.7.3 Ruby Modules

Ruby classes serve as namespace encapsulations, as do the classes of other languages that support object-oriented programming. Ruby has an additional naming encapsulation, called a module. Modules typically define collections of methods and constants. So, modules are convenient for encapsulating libraries of related methods and constants, whose names are in a separate namespace so there are no name conflicts with other names in a program that uses the module. Modules are unlike classes in that they cannot be instantiated or subclassed and do not define variables. Methods that are defined in a module include the module's name in their names. For example, consider the following skeletal module definition:

```
~~~ruby
module MyStuff
  PI = 3.14159265
  def MyStuff.mymethod1 (p1)
    . . .
  end
  def MyStuff.mymethod2 (p2)
    . . .
  end
end
~~~
```

Assuming the `MyStuff` module is stored in its own file, a program that wants to use the constant and methods of `MyStuff` must first gain access to the module. This is done with the `require` method, which takes the file name in the form of a string literal as a parameter. Then, the constants and methods of the module can be accessed through the module's name. Consider the following code that uses our example module, `MyStuff`, which is stored in the file named `myStuffMod`:

```
~~~ruby
require 'myStuffMod'
. . .
MyStuff.mymethod1 (x)
. . .
~~~
```

Modules are further discussed in Chapter 12.

# ## SUMMARY

The concept of abstract data types, and their use in program design, was a milestone in the development of programming as an engineering discipline. Although the concept is relatively simple, its use did not become convenient and safe until languages were designed to support it.