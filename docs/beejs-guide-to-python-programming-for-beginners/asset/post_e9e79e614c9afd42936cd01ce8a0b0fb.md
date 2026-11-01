
Ignoring the `*objects` for now, look at all those keyword arguments... in the docs, they have `=` followed by some value. This indicates the default value if you don't specify one otherwise. In other words, they're optional keyword arguments.

You can see that `print()` ends each line with a newline `\n` unless we tell it to end the line with some other string.

For now, it's enough to know that these exist and how to call them. Later on, we'll talk about how to write our own.

## 10.10 Interlude: Evaluation Strategies

If you don't want to read this section, it's OK to skip. But it's more fun if you read it.

Different languages have different behaviors when it comes to passing arguments to functions.

Some of them make copies of the values. Some of them just make it so the parameter name is an alias for the argument name. Some of them give you the option through some keyword.

How the programming language does this is called its evaluation strategy.

Three very common ones are:

- **Call by Sharing:** This is what Python does. When you call a function, the parameters become references to the same objects as their corresponding arguments. This means that if, inside the function, you change the thing the parameter refers to, you'll see that change reflected out in the caller. However, if you assign a new value into a parameter, you will not see the change.

  ```python
def foo(x):
    # Modify the passed-in object. Caller will see this change.
    x[1] = 99

    # Assign a new list into x. The caller will _not_ see this change.
    x = [4, 5, 6]

a = [1, 2, 3]

foo(a)
print(a)  # [1, 99, 3]
  ```

- **Call by Value:** a copy of the argument is made and stored in the parameter. The C programming language, among others, uses this one. (Sometimes people say Python uses Call by Value, but this is technically not accurate since parameters are not copied when they are passed in; only the reference to the argument is copied. You can make Python simulate Call by Value by making a copy of the parameter when calling the function.)

  ```python
# Simulating call-by-value in Python

def foo(x):
    # Modify the passed-in object. The caller would normally see this
    # change, but if they called it with a copy, only the copy will
    # be affected.
    x[1] = 99

a = [1, 2, 3]

# Simulate call-by-value by making a copy
foo(a.copy())

print(a)  # [1, 2, 3]
  ```

```python
locations = get_ship_locations()
print(locations)
#print_grid(locations)
```

That way we can just do one bit and make sure it's working.

### Fun Motto Fact:

Get something working as quickly as possible, no matter how small a piece of the project it is.

### Problem-solving step: Understanding the Problem

For getting the ship locations, looks like we want to have the user enter an X, Y, Z coordinate. Then we want to split that into a list of numbers. And we need to make sure they are int type—remember that `input()` returns a string, so we'll have to convert them to int.

And we repeat that until the user enters "done".

### Problem-solving step: Devising a Plan

Looping until the user enters "done" is a solved problem. We've done that a few times now. Just make a variable for the `while()` condition, and then set it when the user enters "done".

Otherwise, we have to split the string up into a list of 3 numbers, splitting on the comma. Remember how to do that?

Yes, that's right (or no, not right, if you don't remember), it's the `split()` string method. Example:

```python
"1,2,3".split(',')  # produces list ["1", "2", "3"]
```

But that's not enough. As we noted, we need to convert that list from a list of strings to a list of numbers. Remember how to convert a string to a number? Yes, with the built-in `int()` function!

```python
int("2") == 2  # True!
```

### Problem-solving step: Carrying Out the Plan

Let's get coding!

```python
def get_ship_locations():
    """
    Ask the user to enter a number of X, Y, Z ships coordinates.
    Returns a list of all the coordinates.
    """
    done = False  # True when the user asks to be done

    locations = []  # Master list of all ship positions

    while not done:
        xyz = input('Enter ship location x,y,z (or "done"): ')
        if xyz == "done":
            done = True
        else:
            # Get a list of the x,y,z coordinates
            xyz_list = xyz.split(',')
            # Convert to integers
            for i, v in enumerate(xyz_list):
                xyz_list[i] = int(v)
            # Build the master list
            locations.append(xyz_list)

    return locations

locations = get_ship_locations()
print(locations)
#print_grid(locations)
```

If we give that a run, we see something like this:

```text
Enter ship location x,y,z (or "done"): 1,2,3
Enter ship location x,y,z (or "done"): 4,5,6
Enter ship location x,y,z (or "done"): done
[[1, 2, 3], [4, 5, 6]]
```

There's our list of lists holding the ships' coordinates! It's ready to feed into the `print_grid()` function. But first, we'd better think about that for a bit.

One more thing: if you were looking closely, you saw the big multiline string at the beginning of the function describing what the function does. This is called a docstring and it's a comment that gives overall information about the function. Automatic documentation generators can extract these and build documentation for you, just like you can get with the `help()` function in the REPL.

### Problem-solving step: Understanding the Problem

All righty. What do we need to do for this second part of printing out the grid of distances between the ships?

There are sort of three big pieces here.

- We need to print out a grid.
- We need the first row and first column to list out ship numbers so we can cross-reference.
- We need to compute the distance and print that.

### Problem-solving step: Devising a Plan

```python
print(f'{i:8}', end="")
for j in range(num_ships):
    dist = 99.99
    print(f'{dist:8.2f}', end="")
print()
```

And we get this:

```text
    0       1       2
0   99.99   99.99   99.99
1   99.99   99.99   99.99
2   99.99   99.99   99.99
```

Er, well, that's almost right. The top row is shifted one column left. We need to stick 8 blank spaces in before it to scooch it over. So let's just do it, using string multiplication to make us 8 spaces:

```python
print(" " * 8, end="")   # <-- Add this

for i in range(num_ships):
    print(f'{i:8}', end="")
print()
```

And now we have this:

```text
        0       1       2
0   99.99   99.99   99.99
1   99.99   99.99   99.99
2   99.99   99.99   99.99
```

which is looking right on. Except that all the distances are listed as 99.99. Let's get that out of there and replace it with the real distance between the ships.

### Problem-solving step: Devising a Plan

Distance! We see the distance formula up there at the top, repeated here:

d = √(x₀ − x₁)² + (y₀ − y₁)² + (z₀ − z₁)²

How do we turn that into code?

We could use `math.sqrt()` to get the square root, and `math.pow()` to square the numbers.

### Problem-solving step: Carrying Out the Plan

Here's computing the distance between points p0 and p1 (both of which are lists of X,Y,Z triples) using `math.pow()`:

```python
d = math.sqrt(
    math.pow(p0[0] - p1[0], 2) +  # difference in Xs
    math.pow(p0[1] - p1[1], 2) +  # difference in Ys
    math.pow(p0[2] - p1[2], 2)    # difference in Zs
)
```

And here's option two:

```python
dx = p0[0] - p1[0]  # difference in the Xs
dy = p0[1] - p1[1]  # difference in the Ys
dz = p0[2] - p1[2]  # difference in the Zs

d = math.sqrt(dx*dx + dy*dy + dz*dz)
```

Which do you prefer? Both should give equivalent answers.

In mathematical notation, two variables next to each other like m₁ m₂, above, indicate multiplication.

And for r², a simple equivalent is r × r.

So we can convert that whole equation to:

F = G * (m1 * m2) / (r * r)

where m1 is the mass of one planet, m2 is the mass of the other planet and r is the distance between them.

So far so good.

But what's G? It's the gravitational constant:

G = 6.67430 × 10⁻¹¹

That's written in scientific notation, but we can do the same thing in Python:

G = 6.67430e-11

That should be enough to go on. Write the function and call it with a variety of different values.

Here are some sample values so you can see if your code is working:

| m1 | m2 | r | result |
|---|---|---|---|
| 10 | 20 | 30 | 1.48317e-11 |
| 10 | 40 | 30 | 2.96635e-11 |
| 100 | 5 | 10 | 3.33714e-10 |

(Solution¹⁴.)

## 10.13 Summary

Functions are a super-important part of programming and a highly valuable tool to have at your disposal.

You can use them to break up code into smaller, more manageable pieces. You can also use them to create standalone, reusable pieces of code.

Python comes with a pile of built-in functions, and it pays to know what they are (so you don't reinvent them yourself!)

Finally, you also learned that function arguments come in two flavors: positional and keyword. We'll revisit more of that topic later.

But now: well-deserved break time!
