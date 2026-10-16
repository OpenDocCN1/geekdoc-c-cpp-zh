Another structured form of iteration is provided by an **iterator**. Typically found in object-oriented languages, an iterator is an object that is associated with a collection, such as an array, a list, a set, or a tree. The programmer opens an iterator on a collection and then visits all of its elements by running the iterator’s methods in the context of a loop. For example, the following Java code segment uses an iterator to print the contents of a list, called `exampleList`, of strings:

```
Iterator<String> iter = exampleList.iterator()
while (iter.hasNext())
    System.out.println(iter.next());
```

The iterator-based traversal of a collection is such a common loop pattern that some languages, such as Java, provide syntactic sugar for it, in the form of an **enhanced for loop**:

```
for (String s : exampleList)
    System.out.println(s);
```

We can use this type of loop to further simplify the Java code for computing the sum of either an array or a list of integers, as follows:

```
int sum = 0;
for (int data : list){
    if (data < 0)
        data = -data;
    sum += data;
}
```

Iterators are covered in detail in Chapter 5.

Another powerful mechanism for structuring control is the **procedure**, sometimes also called a **subprogram** or **subroutine**. This allows a programmer to consider a sequence of actions as a single action that can be called or invoked from many other points in a program. Procedural abstraction involves two things. First, a procedure must be defined by giving it a name and associating with it the actions that are to be performed. This is called **procedure declaration**, and it is similar to variable and type declaration, mentioned earlier. Second, the procedure must actually be called at the point where the actions are to be performed. This is sometimes also referred to as procedure **invocation** or procedure **activation**.

As an example, consider the sample code fragment that computes the greatest common divisor of integers u and v. We can make this into a procedure in Ada with the procedure declaration as given in Figure 1.6.

```
procedure gcd(u, v: in integer; x: out integer) is
    y, t, z: integer;
begin
    z := u;
    y := v;
    loop
        exit when y = 0;
```

**Figure 1.6** An Ada gcd procedure *(continues)*