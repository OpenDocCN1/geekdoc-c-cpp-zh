```
print(x.antelopes)  # 10!
```

Remember that when you call a function, it is assigning the argument into the parameter name, so both of them refer to the same object. That is, in the code above, o refers to the same object x does, just as if we'd done an assignment with o = x.

# 11.11 Objects and None

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

# 11.12 Testing for Attributes

Sometimes at runtime, you want to see if an object has an attribute or not. Or maybe you have the attribute name as a string and you want to get or set that attribute on an object.

Three built-in functions help make this happen:

+   - hasattr() tests to see if an attribute exists on an object.