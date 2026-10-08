When you are working on an advanced IDE such as Visual C# Express, the keyword, 'using' will end up creating parts of the trivial code in your stead. In this example, it was used for creating a class for you. It also imported the namespaces that are necessary or are expected to be used.

In this example, three namespaces have been imported into the program. Each of these namespaces contains some useful classes. The Console class has been used in this program, and it belongs to the System namespace.

You will also notice that the application gets its very own namespace as shown below.

# 'Namespace’ ConsoleApplication1

This is now the primary namespace for this application. By default, any new classes created will become a part of it. It is possible to modify this and create other classes under another namespace. If you want to do so, you need to import this namespace into your application with the help of the ‘using’ statement.

For the next step, the class has to be defined. C# is an object oriented language. As a result, all lines of code which actually performs something will have to be kept inside a class. For this example, the class has been named Program as shown below.

# 'Class’ Program

It is possible to increase the number of classes in the same application. However, that was not necessary for this program. A class is capable of containing a number of methods, properties, and variables. However, that will be discussed later. In this program, there is only a single method which is declared as follows.

```
'Static void Main’ (string [ ] args)
```

The first word of this line is static, and it is a keyword. It instructs the program to keep the method accessible without causing the class to instantiate. The void keyword tells the program what should be returned by the program which in this case is nothing.

The word, Main, is simply the name given to this method. In this case, it serves as what is known as the entry-point of the application. In other words, it will be the