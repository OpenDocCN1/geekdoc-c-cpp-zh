
What we're starting to delve into here is the world of Object-Oriented Programming. To discuss everything about it would definitely be information overload, so we're just going to start with the basics here, and revisit some of the concepts later.

A bit of terminology here, following up on the starship example from above.

First of all, we're going to construct new starship objects that hold all the information about a single ship.

When the object is constructed, it is done based on a blueprint. We call this blueprint a class.

So we're going to define a blueprint for a starship in a class, and then we're going to build multiple, different starships based on that class.

Let's do this as simple as possible to start. It's not going to be a common way of doing things, but it's a place to get your feet wet. We'll fix it soon.

First of all, we'll define a new class. Remember, this is just the blueprint for starships—it's not a starship itself.

Class names use camel case by convention. Let's define that starship class!

```python
class StarShip:
    pass
```

...that's it? What's that pass in there?

Okay, you got me. I did say we were going to start simple (and not quite Right), in my defense. What we have there is a class StarShip, except it's like a blank blueprint. There's nothing in it.

The keyword pass means "do nothing" in Python. It's just there to indicate to Python that there's no body inside this class.

Random Terminology Facts: We also say a starship object is an instance of the StarShip class.

Constructing a new starship object is also referred to as instantiating the object from the class.

Let's go on to make a couple of objects from the blueprint.

```python
class StarShip:
    pass

s0 = StarShip()
s1 = StarShip()
s2 = StarShip()
```

By putting parens after the class name, we're telling Python that we are creating a new starship object from the StarShip class. In fact, we made three of them and saved a reference to each in s0, s1, and s2. Of course, none of them have names or locations, but we'll remedy that shortly.

If we print one, we get something like this:

```python
print(s1)  # <__main__.StarShip object at 0x7fa11828c8e0>
```

Not so pretty. But we'll make that better soon, as well.

## 11.5 Making Different StarShips

Problem-solving step: Understanding the Problem.

In the previous example, all our starship objects were identical and contained no information.

What we need is a way to pass that information in when the starships are constructed.

We do this by defining a special function inside the class.

Another Fun Terminology Fact: functions declared inside classes are called methods.

This special function is always named __init__() (with the dunders) and is called the constructor.

Let's add a constructor to our StarShip class that allows us to pass in a ship name when the ship is constructed:

```python
class StarShip:
    def __init__(self, shipname):  # The constructor
        self.name = shipname

s0 = StarShip("MCRN Tachi")
s1 = StarShip("Red Dwarf")
s2 = StarShip("USCSS Nostromo")
```

Whoa, now... that's a lot of hard-to-read punctuation³ to sift through.

And there's that crazy self parameter to the function, whatever that means!

Let's start with self⁴. This is one of the hardest concepts to grok about in this chapter, so we'll spend some time on it.

Remember how the class is the blueprint, and the objects are made from that blueprint?

And how after they're constructed, you get a reference back to that newly-minted object? (These are the references we were storing in s0, s1, and s2.)

Well, what about the object that's being constructed right now inside the __init__() method? It already exists but isn't fully initialized yet. But inside the constructor, we have a reference to that object that is being built right now. And that reference is in self.

self means "the object that this method is operating on".

What's weird is that when we instantiated the starships, we only passed one argument to __init__().

```python
s0 = StarShip("MCRN Tachi")
```

When clearly __init__() has two parameters: self and name. What gives?

```python
def __init__(self, shipname):  # The constructor
```

Doesn't the number of arguments need to match the number of parameters?

It does! But Python's doing something sneaky behind your back, here. When a method has been called for a particular object, Python automatically fills in the first parameter with the object that is being operated on. We don't have to worry about it.

Python then takes the arguments we did pass and tacks them on after that.

Let's take a look at that constructor again:

```python
class StarShip:
    def __init__(self, shipname):  # The constructor
        self.name = shipname

s0 = StarShip("MCRN Tachi")
```

This is a really common pattern, so let's make sure we understand what's going on here. In particular, there's a weird dot after self. What does that mean? But before we get there, let's look at shipname.

When we create our new starship s0, we pass in the name "MCRN Tachi". This calls the constructor __init__().

Python automatically puts a reference to the object that's now being constructed into self. And then it copies the string "MCRN Tachi" to the shipname parameter of the function. So shipname is "MCRN Tachi".

And now we're to the guts of the thing. self.name? The saga continues!

And we could modify the location of the ship this way, as well:

```python
s0.location[1] = 99

print(s0.location)  # [0, 99, 0]
```

This is important! Even though we're changing the values for the attributes of s0, the attributes of the other objects (like s1 and s2) remain unchanged! (Until we explicitly change them.)

We've successfully bundled all the information about a single ship into this single object. Nice and consolidated.

## 11.8 More on Methods

Problem-solving step: Understanding the Problem.

Remember that methods are functions that are connected to the object. Just like you could think of attributes as things the object has, you can think of methods like things the object does.

Let's add another method to set the ship location.

```python
class StarShip:
    def __init__(self, name):  # The constructor
        self.name = name
        self.location = [0, 0, 0]  # <-- Add this

    def set_location(self, x, y, z):
        """Set a ship's location to x,y,z"""

        self.location[0] = x
        self.location[1] = y
        self.location[2] = z

s0 = StarShip("MCRN Tachi")

print(s0.location)  # [0, 0, 0]

s0.set_location(10, 20, 30)

print(s0.location)  # [10, 20, 30]
```

On line 6, we define our new method, set_location(). Importantly, notice the first parameter is self, which will be initialized to represent the object we're setting the location of. (That is, when we call s0.set_location(), self will be set to refer to s0 inside set_location().)

Fun Debugging Fact: If you get an error about the incorrect number of arguments to your method, make sure you have self as the first parameter!

Then on line 17, when we call set_location() on s0, self gets set to s0, and x, y, and z get set to 10, 20, and 30, respectively.

Attributes!

## 11.9 Pretty Printing

Right now when we print one of our starship objects, Python prints something like this on the screen:

```python
<__main__.StarShip object at 0x7fa11b28c9e0>
```

Not particularly useful. Let's override that functionality and have it print something nicer.

Go ahead and add this method to the StarShip class:

```python
def __str__(self):
    """Return string representation of this object."""
    return f'{self.name}: {self.location}'
```

The __str__() method returns a string to use any time an object is printed.

Now if we build three new ships and print them all:

```python
s0 = StarShip("Rocinante")
s1 = StarShip("Red Dwarf")
s2 = StarShip("USCSS Nostromo")

s0.set_location(10, 20, 30)
s1.set_location(40, 50, 60)
s2.set_location(70, 80, 90)

print(s0)
print(s1)
print(s2)
```

We get some nice output, like this:

```
Rocinante: [10, 20, 30]
Red Dwarf: [40, 50, 60]
USCSS Nostromo: [70, 80, 90]
```

Perfect!

## 11.10 Objects are Mutable

When you assign one object to another, you don't get a second object. You get another reference to the first object. Just like happens with lists and dictionaries.

Or, another way, doing an assignment with an object does not result in a new object. Both variables are names for the same object. (Check out Appendix C for details.)

```python
class Forest:
    pass

x = Forest()  # Construct a new object
y = x

x.antelopes = 4

print(y.antelopes)  # 4, since y and x refer to the same object
```

This means you can pass objects to functions as arguments, and the function can change the values in the object's attributes.

```python
def set_antelopes_to_10(o):
    o.antelopes = 10

class Forest:
    pass

x = Forest()
x.antelopes = 4

set_antelopes_to_10(x)
```
