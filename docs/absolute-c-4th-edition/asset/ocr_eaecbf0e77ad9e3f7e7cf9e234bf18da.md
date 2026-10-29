# Display 19.2 Bidirectional and Random Access Iterator Use (part 2 of 2)

```
28  p++;
29  cout << *p << endl;
30  p--;
31  cout << *p << endl;
32
33 }
```

> This works for any bidirectional iterator.

# SAMPLE DIALOGUE

```
container[0] == A
container[1] == B
container[2] == C
container[3] == D
The third entry is C
The third entry is C
The third entry is C
Back to container[0].
which has value A
Two steps forward and one step back:
B
C
B
```

The increment and decrement operators can be used in either prefix (++p) or postfix (p++) notation. In addition to changing p, they also return a value. The details of the value returned are completely analogous to what happens with the increment and decrement operators on int variables. In prefix notation, first the variable is changed and then the changed value is returned. In postfix notation, the value is returned before the variable is changed. We prefer not to use the increment and decrement operators as expressions that return a value; we use them only to change the variable value.

The following lines from Display 19.2 illustrate the fact that with vector iterators you have random access to the elements of a vector, such as container:

```
iterator p = container.begin();
cout << "The third entry is " << container[2] << endl;
cout << "The third entry is " << p[2] << endl;
cout << "The third entry is " << *(p + 2) << endl;
```

Random access means that you can go directly to any particular element in one step. We have already used container[2] as a form of random access to a vector. This is simply the square bracket operator that is standard with arrays and vectors. What is new is that you can use this same square bracket notation with an iterator. The expression p[2] is a way to obtain access to the element indexed by 2.