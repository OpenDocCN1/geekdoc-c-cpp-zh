# Generics are type-safe

![](bbox=[0.13, 0.15, 0.2, 0.27])

When you declare an array, you must specify the exact type of data it can hold. If you specify int, the array can’t hold anything other than ints or other numeric types that C# can convert implicitly to int. You see compiler errors at build-time if you try to put the wrong kind of data into an array. Thus the compiler enforces type-safety, enabling you to fix a problem before it ever gets out the door.

A compiler error beats the heck out of a runtime error. In fact, a compiler error beats everything except a royal flush or a raspberry sundae. Compiler errors are useful because they help you spot problems now.

![](bbox=[0.13, 0.35, 0.2, 0.47])

The old-fashioned nongeneric collections aren’t type-safe. In C#, everything IS_A Object because Object is the base type for all other types, both value-types and reference-types. But when you store value-types (numbers, chars, bools, and structs) in a collection, they must be boxed going in and unboxed coming back out. It’s as though you’re putting items in an egg carton and having to stuff them inside the eggs so that they fit and then breaking the eggshells to get the items back out. (Reference-types such as string, Student, and BankAccount don’t undergo boxing.)

The first consequence of nongenerics lacking type-safety is that you need a cast, as shown in the following code, to get the original object out of the ArrayList because it’s hidden inside an egg, er, Object:

```
ArrayList aList = new ArrayList();
// Add five or six items, then ...
string myString = (string)aList[4];  // Cast to string.
```

![](bbox=[0.13, 0.6, 0.2, 0.72])

Fine, but the second consequence is this: You can put eggs in the carton, sure. But you can also add marbles, rocks, diamonds, fudge — you name it. An ArrayList can hold many different types of objects at the same time. So it’s legal to write this:

```
ArrayList aList = new ArrayList();
aList.Add("a string");      // string -- OK
aList.Add(3);               // int -- OK
aList.Add(aStudent);        // Student -- OK
```

However, if you put a mixture of incompatible types into an ArrayList (or another nongeneric collection), how do you know what type is in, say, aList[3]? If it’s a Student and you try to cast it to string, you get a runtime error. It’s just like Harry Potter reaching into a box of Bertie Bott’s Every Flavor Beans: He doesn’t know whether he’ll grab raspberry beans or earwax.

![](bbox=[0.13, 0.85, 0.2, 0.97])

To be safe, you have to resort to using the is operator (discussed in Book II) or the alternative, the as operator: