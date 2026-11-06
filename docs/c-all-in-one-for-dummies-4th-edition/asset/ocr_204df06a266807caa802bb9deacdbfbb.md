When you run this code, you see the following output:

```
~~~
I'm smart!
I'm beautiful!
~~~
```

In the preceding code, the class Derived inherited the functions of both classes Mom and Dad. Because it did, the compiler allows a Derived instance, child, to call both functions. You use this approach to derive from multiple classes:

```
~~~
class Derived : public Mom, public Dad
~~~
```

You start with the base classes to the right of the single colon, as with a single inheritance, and separate the classes with a comma. You also precede each class with the type of inheritance, public.

# ## Setting access in multiple inheritance

As with single inheritance, you can use inheritance other than public. But you don't have to use the same access for all the classes. For example, the following, although a bit confusing, is acceptable:

```
~~~
class Derived : public Mom, protected Dad
~~~
```

This means that public members derived from Dad are now protected in the Derived class, which also means that users can't call the methods inherited from Dad, nor can they access any properties inherited from Dad. If you used this type of inheritance in Listing 4-2, this line would no longer work:

```
~~~
child.Beauty();
~~~
```

If you try to compile it, you see the following error, because the Beauty() member is protected now:

```
~~~
'void Dad::Beauty()' is inaccessible
~~~
```

![](bbox=[0.173, 0.659, 0.232, 0.718])

When you work with multiple inheritance, be careful that you understand what your code is doing. Although it may compile correctly, it still may not function correctly, leading to the famous creepy-crawly thing called a bug.

# ## Seeing multiple inheritance go wrong

Strange, bizarre, freaky things can happen with multiple inheritance. If both base classes have a property called Bagel, the compiler gets confused. Suppose you