
```
print(x.antelopes)  # 10!
```

Remember that when you call a function, it is assigning the argument into the parameter name, so both of them refer to the same object. That is, in the code above, o refers to the same object x does, just as if we'd done an assignment with o = x.

## 11.11 Objects and None

We've already seen that variables can point to the value None to indicate nothing.

This gets commonly used with objects to indicate some "not found" or error condition.

For example, let's have a list of objects and a function to search them by name. The function should return the object that has a name attribute that matches the name parameter to the function.

But a question should naturally arise! What if there is no object by that name in the list? What should the function return? None is a prime candidate here.

```
class Person:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return self.name

def get_person_by_name(person_list, name):
    """Return a person object with this name, or None if not found"""
    for p in person_list:
        if p.name == name:
            # If we found them, return the object
            return p

    # If we got here, we didn't find anyone by that name
    return None

person_list = [
    Person("Annie"),
    Person("Beej"),
    Person("Chris")
]

p = get_person_by_name(person_list, "Chris")

print(p)  # "Chris"

p = get_person_by_name(person_list, "Dave")

if p is None:
    print("Dave's not here.")
```

## 11.12 Testing for Attributes

Sometimes at runtime, you want to see if an object has an attribute or not. Or maybe you have the attribute name as a string and you want to get or set that attribute on an object.

Three built-in functions help make this happen:

- hasattr() tests to see if an attribute exists on an object.
- getattr() returns the value of an attribute, optionally returning a default value if the attribute doesn't exist.
- setattr() sets the value of an attribute, creating it if it doesn't exist.

This gives you more flexibility in writing your objects, because then you can have optional attributes on them.

Let's demo!

```
class Foo:
    pass

f = Foo()
f.bar = 12

print(hasattr(f, "bar"))    # True
print(hasattr(f, "frotz"))  # False

print(getattr(f, "bar"))            # 12
print(getattr(f, "frotz", None))    # None, since attr frotz doesn't exist

setattr(f, "frotz", 99)  # Just like saying "f.frotz = 99"

print(f.frotz)  # 99
```

I wouldn't say that these functions get a lot of day-to-day use, but they're a powerful thing to add to your toolkit.

## 11.13 Chapter Project

In case you've forgotten, review the chapter project specification at the beginning of this chapter.

### Problem-solving step: Understanding the Problem.

Looks like we need to store information about a number of theaters, as well as information about a number of movies.

And a movie might be showing in multiple theaters simultaneously.

### Problem-solving step: Devising a Plan

There are a lot of ways to store this data. But since this chapter is all about classes and objects, how about we use those?

Looks like we should have a Theater class to handle information about each theater.

And a Movie class to handle information about each movie.

And a theater can be showing several movies, so we can give it an attribute that is a list of movies that is currently showing there.

We'll also keep a list of all the theaters and a list of all the movies, as well.

### Problem-solving step: Carrying Out the Plan

Here's a theater class. We pass a name to the constructor but initialize the movies to an empty list. We can fill them in later.

```
class Theater:
    """Holds all the information about a specific theater."""
    def __init__(self, name):
        self.name = name
        self.movies = []
```

and a movie class:

```
class Movie:
    """Holds all the information about a specific movie."""
    def __init__(self, name, duration, genre):
        self.name = name
        self.duration = duration
        self.genre = genre
```

So far so good.

Now we need to instantiate a bunch of movies so that we can add them to the theaters’ .movie lists.

There are a couple of things we could do.

We could use one variable per movie, but that’s a bit unwieldy. Let’s use some kind of collection, like a list! We’ll make one for all the movies and all the theaters. Go ahead and add your favorites.

```
movies = [
    Movie("Star Wars", 125, "scifi"),
    Movie("Shaun of the Dead", 100, "romzomcom"),
    Movie("Citizen Kane", 119, "drama")
]

theaters = [
    Theater("McMenamin's Old St. Francis Theater"),
    Theater("Tin Pan Theater"),
    Theater("Tower Theater")
]
```

Take a look in there to see what we’ve done. Notice that movies is a list, and inside the list, while we’re initializing it, we’re constructing new Movie objects.

And we do the same thing with theaters. It’s a list of newly-constructed Theater objects.

Nextly, we need to associate those movies with the theaters that are showing them.

Remember that each Theater object has a list of movies in its .movies attribute. So we need to append the movies to that list.

This next bit is a little cryptic, so make sure

```
# McMenamin's is showing Star Wars and Shaun of the Dead
theaters[0].movies.append(movies[0])
theaters[0].movies.append(movies[1])
```

What’s that saying?

Well, take it a bit at a time, each line from left to right.

What’s theaters[0]?

If we look in our theaters list, we see that’s McMenamin’s.

And then we get its movie list with theaters[0].movies.

Its movies list is a list, so we can use the .append() list method to add a movie to it. But which movie to append?

We append movies[0]... and if we look in our movies list, we see that’s Star Wars.

So theater[0] is McMenamin’s, and movies[0] is Star Wars.

That means the first line, above, is saying, “Append ‘Star Wars’ to McMenamin’s list of currently showing movies.”

And the line below that is saying, “Append ‘Shaun of the Dead’ to McMenamin’s list of currently showing movies.”

Let’s do some more. What do each of these lines do?

```
# Tin Pan is showing Shaun of the Dead and Fastest Indian
theaters[1].movies.append(movies[1])
theaters[1].movies.append(movies[2])

# Tower is showing all three
theaters[2].movies.append(movies[0])
theaters[2].movies.append(movies[1])
theaters[2].movies.append(movies[2])
```

What we’ve done here, effectively, is linked up all the movie objects with their respective theaters.

Notice how movies are listed in multiple theaters. For example movies[0] (Star Wars) is in theaters[0] (McMenamin’s) and also in theaters[2] (Tower).

Does that mean there are two copies of the Star Wars Movie object? Since it’s in two theaters?

Think carefully!

No, there’s just one! The one we created back on line 15! Since it’s an object, making a “copy” through assignment (or with .append()) just makes another reference to the same object. There’s only one, but it’s referred to by two Theater objects. And also referred to by the movies list. So many references to the same object for good memory savings.

Now we want to print out all the theaters and their showtimes. I’m going to make a helper function here to print a single theater’s data. We’ll pass in a reference to a theater object, print its name, and then print the data for all the movies in its .movies list.

```
def print_theater(theater):
    """Print all the information about a theater."""
    print(f'{theater.name} is showing:')
    for m in theater.movies:
        print(f'    {m.name} ({m.genre}, {m.duration} minutes)')
```

And lastly, all we have to do is call print_theater() for all the theaters in our theaters list:

```
# Main code
for t in theaters:
    print_theater(t)
```

There we have it! (Solution⁶)

### Problem-solving step: Looking Back.

Check out how we looked at the problem description (which basically said “theaters show movies, and a movie might be shown at multiple theaters”) and mapped that into two classes to hold the information per theater and per movie.

Notice how the classes keep all the information for a theater or movie in a self-contained single object.

Nice and clean, plus it’s easy to pass around a reference to an object if another function wants to use it.

What are some shortcomings?

Those lines where we add the movies to theaters are pretty hard to read. And they refer to things like movies[0] instead of referring to them by name.
