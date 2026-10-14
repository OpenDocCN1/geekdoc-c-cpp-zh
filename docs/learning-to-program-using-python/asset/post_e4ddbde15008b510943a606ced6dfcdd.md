
in a way that works best; maybe you don’t need to have a full-blown class with initialization code and methods to just return a calculation. With Python, you can get as technical as you want.

## 15.2 How Are Classes Better?

Imagine you have a program that calculates the velocity of a car in a two-dimensional plane using functions. If you want to make a new program that calculates the velocity of an airplane in three dimensions, you can use the concepts of your car functions to make the airplane model work, but you’ll have to rewrite many of the functions to make them work for the vertical dimension, especially if you want to map the object in a 3-D space. You may be lucky and be able to copy and paste some of them, but for the most part you’ll have to redo much of the work.

Classes let you define an object once, then reuse it multiple times. You can give it a base function (called a method in OOP parlance) then build upon that method to redefine it as necessary. It also lets you model real-world objects much better than using functions.

For example, you could make a tire class that defines the size of the tire, how much pressure it holds, what it’s made of, etc., then make methods to determine how quickly it wears down based on certain conditions. You can then use this tire class as part of a car class, a bicycle class, or whatever. Each use of the tire class (called instances) would use different properties of the base tire object. If the base tire object said it was just made of rubber, perhaps the car class would "enhance" the tire by saying it had steel bands or maybe the bike class would say it has an internal air bladder. This will make more sense later.

## 15.3 Improving Your Class Standing

Several concepts of classes are important to know.

- 1. Classes have a definite namespace, just like modules. Trying to call a class method from a different class will give you an error unless you qualify it, e.g. `spamClass.eggMethod`.

- 2. Classes support multiple copies. This is because classes have two different objects: class objects and instance objects. Class objects give the default behavior and are used to create instance objects. Instance objects are the objects that actually do the work in your program. You can have as many instance objects of the same class object as you need. Instance objects are normally marked by the keyword `self`, so a class method could be `Car.Brake()` while a specific instance of the `Brake()` method would be marked as `self.Brake()`. (I'll cover this in more depth later).

- 3. Each instance object has its own namespace but also inherits from the base class object. This means each instance has the same default namespace components as the class object, but additionally each instance can make new namespace objects just for itself.

- 4. Classes can define objects that respond to the same operations as built-in types. So class objects can be sliced, indexed, concatenated, etc. just like strings, lists, and other standard Python types. This is because everything in Python is actually a class object; we aren't actually doing anything new with classes, we're just learning how to better use the inherent nature of the Python language.

Here's a brief list of Python OOP ideas:

- The class statement creates a class object and gives it a name. This creates a new namespace.
- Assignments within the class create class attributes. These attributes are accessed by qualifying the name using dot syntax: `ClassName.Attribute`.
- Class attributes export the state of an object and its associated behavior. These attributes are shared by all instances of a class.
- Calling a class (just like a function) creates a new instance of the class. This is where the multiple copies part comes in.
- Each instance gets ("inherits") the default class attributes and gets its own namespace. This prevents instance objects from overlapping and confusing the program.
- Using the term `self` identifies a particular instance, allowing for per-instance attributes. This allows items such as variables to be associated with a particular instance.

## 15.4 So What Does a Class Look Like?

Before we leave this particular tutorial, I'll give you some quick examples to explain what I've talked about so far. Assuming you're using the Python interactive interpreter, here's how a simple class would look like.

```python
# Listing 15.1: Defining a class
>>> class Hero: #define a class object
...     def setName(self, value):  #define class methods
...         self.name = value   #self identifies a particular instance
...     def display(self):
...         print self.name #print the data for a particular instance
```

There are a few things to notice about this example:

- 1. When the class object is defined, there are no parentheses at the end; parentheses are only used for functions and methods. However, see Section 15.5 for a caveat.

- 2. The first argument in the parentheses for a class method must be `self`. This is used to identify the instance calling the method. The Python interpreter handles the calls internally. All you have to do is make sure `self` is where it's supposed to be so you don't get an error. Even though you must use `self` to identify each instance, Python is smart enough to know which particular instance is being referenced, so having multiple instances at the same time is not a problem. (`self` is similar to `this`, which is used in several other languages like Java).

- 3. When you are assigning variables, like “self.name”, the variable must be qualified with the "self" title. Again, this is used to identify a particular instance.

So, let's make a few instances to see how this works:

```python
# Listing 15.2: Creating class instances
>>> x = Hero()
>>> y = Hero()
>>> z = Hero()
```

Here you’ll notice that parenthesis make an appearance. This is to signify that these are instance objects created from the Hero class. Each one of these instances has the exact same attributes, derived from the Hero class. (Later on I’ll show you how to customize an instance to do more than the base class).

Now, let's add some information.

```python
# Listing 15.3: Adding data to instances
>>> x.setName("Arthur, King of the Britons")
>>> y.setName("Sir Lancelot, the Brave")
>>> z.setName("Sir Robin, the Not-Quite-So-Brave-As-Sir-Lancelot")
```

These call the **setName()** method that sits in the Hero class. However, as you know by now, each one is for a different instance; not only do x, y, and z each have a different value, but the original value in Hero is left untouched.

If you now call the **display()** method for each instance, you should see the name of each hero.

```python
# Listing 15.4: Displaying instance data
>>> x.display()
Arthur, King of the Britons
>>> y.display()
Sir Lancelot, the Brave
>>> z.display()
Sir Robin, the Not-Quite-So-Brave-As-Sir-Lancelot
```

You can change instance attributes "on the fly" simply by assigning to *self* in methods inside the class object or via explicitly assigning to instance objects.

```python
# Listing 15.5: Modifying instances
>>> x.name = "Sir Galahad, the Pure"
>>> x.display()
Sir Galahad, the Pure
```

That’s probably enough for this lesson. I’ll cover the rest of classes in the next chapter but this is hopefully enough to give you an idea of how useful classes and OOP in general can be when programming. The vast majority of languages in current use implement OOP to one extent or another, so learning how to use classes and objects will help you out as you gain knowledge. Thankfully Python implements OOP in a reasonable way, so it’s relatively painless to learn in Python rather than something like C++, at least in my experience.

### 15.5 “New-style” classes

Starting with Python 2.2, a new type of class was developed for Python. This new class provided a way for programmers to create a class derived, directly or indirectly, from a built-in Python type, such as a list, string, etc.

You can make a new class like the above examples, where no parenthesis are used. However, you can also expressly inherit your new class from the *object* class, or you can derive a new class from one of the built-in types. Listing 15.6 shows how this would look. Deriving your custom classes from *object* is a good idea, since Python 3.x only uses the “new-style” and omitting *object* can cause problems. More information can be found at Introduction To New-Style Classes In Python and Python’s New-style Classes.

```python
# Listing 15.6: New-style classes
class NewStyleUserDefinedClass(object):
    pass
class DerivedFromBuiltInType(list):
    pass
```
