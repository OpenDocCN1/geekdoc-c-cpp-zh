Blocks are somewhat similar to methods and functions in that they are a way of bundling up a number of expressions for later execution. Blocks, however, can be stored as variables and passed as arguments. We can create block variables as shown:

```
returnType (^blockName)(argument, types);
```

For example, let’s declare a block variable named sum that returns an integer and takes two integer arguments:

```
int (^sum)(int, int);
```

You can define a literal block starting with the caret (^) and then declaring the arguments in parentheses and the actual code in curly brackets.

```
sum = ^(int a, int b){return a + b;};
```

Once a block variable is assigned, you can call it just like any other function.

```
NSLog(@"The sum of %d and %d is %d", 5, 6, sum(5, 6));
```

It’s important to note that blocks can capture any data that is in scope when the block is defined. For example, in this sample, addToOffset will take a single argument and add the offset variable to it.

```
int offset = 5;
int (^addToOffset)(int) = ^(int value){return offset + value;};
```

> > **NOTE:** When a block captures a local variable stored on the stack, it treats this variable as a const value. You can read the value but not modify it. If you need to mutate a local variable, you must declare it using the `__block` storage type modifier. Generally, this only applies to local C types and structs. You can already mutate objects, instance variables, and anything else allocated on the heap.

![](bbox=[0.76, 0.728, 1.0, 0.85])

Usually, however, we don’t create or call block variables. Instead, we pass literal blocks to methods and functions as arguments. For example, NSArray has a method, enumerateObjectsUsingBlock:, that takes a single block. This method will iterate through all the objects in the array. For each object, it calls the block, passing in the object, the object’s index, and a reference to a stop value.