```
25     elements.add( pushValue ); // place pushValue on Stack
26   } // end method push
27
28   // return the top element if not empty; else throw EmptyStackException
29   public T pop()
30   {
31     if ( elements.isEmpty() ) // if stack is empty
32       throw new EmptyStackException( "Stack is empty, cannot pop" );
33
34     // remove and return top element of Stack
35     return elements.remove( elements.size() - 1 );
36   } // end method pop
37 } // end class Stack< T >
```

Fig. 21.7 | Stack generic class declaration. (Part 2 of 2.)

Class Stack declares variable elements as an ArrayList<T> (line 7). This ArrayList will store the Stack’s elements. As you know, an ArrayList can grow dynamically, so objects of our Stack class can also grow dynamically. The Stack class’s no-argument constructor (lines 10–13) invokes the one-argument constructor (lines 16–20) to create a Stack in which the underlying ArrayList has a capacity of 10 elements. The one-argument constructor can also be called directly to create a Stack with a specified initial capacity. Line 18 validates the constructor’s argument. Line 19 creates the ArrayList of the specified capacity (or 10 if the capacity was invalid).

Method push (lines 23–26) uses ArrayList method add to append the pushed item to the end of the ArrayList elements. The last element in the ArrayList represents the top of the stack.

Method pop (lines 29–36) first determines whether an attempt is being made to pop an element from an empty Stack. If so, line 32 throws an EmptyStackException (declared in Fig. 21.8). Otherwise, line 35 returns the top element of the Stack by removing the last element in the underlying ArrayList.

Class EmptyStackException (Fig. 21.8) provides a no-argument constructor and a one-argument constructor. The no-argument constructor sets the default error message, and the one-argument constructor sets a custom error message.

```
1  // Fig. 21.8: EmptyStackException.java
2  // EmptyStackException class declaration.
3  public class EmptyStackException extends RuntimeException
4  {
5    // no-argument constructor
6    public EmptyStackException()
7    {
8      this( "Stack is empty" );
9    } // end no-argument EmptyStackException constructor
10
11   // one-argument constructor
12   public EmptyStackException( String message )
13   {
```

Fig. 21.8 | EmptyStackException class declaration. (Part 1 of 2.)