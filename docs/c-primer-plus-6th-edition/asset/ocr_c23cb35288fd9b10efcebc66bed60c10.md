Suppose you want to use a reference return value but don't want to permit behavior
such as assigning a value to accumulate().Just make the return type a const reference:
const free_throws &\naccumulate(free_throws & target, const free_throws & source);

The return type now is const, hence a nonmodifiable lvalue.Therefore, the assignment
is no longer allowed:
accumulate(dup,five) = four; // not allowed for const reference return

What about the other function calls in the program?With a const reference return
type, the following statement would be allowed:
display(team,two);

That's because the formal parameter for display() is also type const free_throws &
But the following statement would not be allowed because the first parameter for
accumulate() is not const:

accumulate(team, three), four);

Is this a great loss? Not in this case because you still do the following:
accumulate(team, three);
accumulate(team, four);

And you could still use accumulate() on the right side of an assignment
statement.

By omitting const, you can write shorter but obscure-looking code.
Usually, you're better off avoiding the addition of obscure features to a design because
obscure features often expand the opportunities for obscure errors. Making the return
type a const reference protects you from the temptation of obfuscation. Occa-
sionally, however, omitting const makes sense. The overloaded << operator discussed
in Chapter 11,"Working with Classes," is an example.

# Using References with a Class Object

The usual C++ practice for passing class objects to a function is to use references. For
instance, you would use reference parameters for functions taking objects of the string,
, istream, ofstream, and ofstream as arguments.

Let's look at an example that the string class and illustrates some different design
choices, some of them bad. The general idea is to create a function that adds a given string
to each end of another string. Listing 8.7 provides three functions that are intended to do
this. However, one of the designs is flawed that it may cause the program to crash or
even compile.