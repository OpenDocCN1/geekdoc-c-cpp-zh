True if the second parameter is twice the first parameter regardless of the sign of either number:

```
~~~ada
function Double (First    : in Integer;
                Second   : in Integer) return Boolean is
   (abs Second = 2 * abs First);
~~~
```

Note that the expression implementing function Double is enclosed in parentheses. A common use of expression functions is within assertions such as preconditions, postconditions, and loop invariants. Replacing complex expressions with well-named function calls can make assertions easier to read. Of course, we can also easily reuse the expression in other assertions.

# ### 2.3 Data Types

A computer program operates on data stored in memory. Our programs reference this data through symbolic names known as *objects*. An object is declared as either variable or constant. In Ada, every object must be of a specific type. The *data type* establishes the set of possible values that an object of that type may take (its domain) and the set of operations that can be performed with those values. For example, an integer type might have a domain consisting of all of the whole numbers between −2, 147, 483, 648 and +2, 147, 483, 647. Operations on these numbers typically include the arithmetic operators (+, −, ×, ÷), equality operators (=, ≠), and relational operators (<, >, ≤, ≥).

The primary predefined types in Ada are Boolean, Character, Integer, Float, *Duration*, and String. You are familiar with most of these types from your prior programming experiences. *Duration* is a real number type used to keep track of time in seconds. As you saw in the examples earlier in this chapter, an Ada variable is declared by writing its name followed by the name of its type. Here are some more examples:

```
~~~ada
Found    : Boolean;
Letter   : Character;
Count    : Integer;
Distance : Float;
~~~
```

Constant declarations are similar but require the addition of the word **constant** and a value:

```
~~~ada
Pay_Taxes : constant Boolean  := True;
Negative  : constant Character := 'N';
Maximum   : constant Integer   := 1_247_962;
-- Note the use of underscores to
~~~
```