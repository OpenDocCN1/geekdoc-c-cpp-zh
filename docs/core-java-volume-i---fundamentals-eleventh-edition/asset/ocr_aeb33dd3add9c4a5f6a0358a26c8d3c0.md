```
~~~java
    else if (args[0].equals("-g"))
        System.out.println("Goodbye,");
    // print the other command-line arguments
    for (int i = 1; i < args.length; i++)
        System.out.println(" " + args[i]);
    System.out.println("!");
}
~~~
```

If the program is called as

```
~~~
java Message -g cruel world
~~~
```

then the args array has the following contents:

```
~~~
args[0]: "-g"
args[1]: "cruel"
args[2]: "world"
~~~
```

The program prints the message

```
~~~
Goodbye, cruel world!
~~~
```

> > **C++ NOTE:** In the main method of a Java program, the name of the program is not stored in the args array. For example, when you start up a program as
> >
> >     java Message -h world
> >
> > from the command line, then args[0] will be "-h" and not "Message" or "java".

# ### 3.10.6 Array Sorting

To sort an array of numbers, you can use one of the sort methods in the Arrays class:

```
~~~java
int[] a = new int[10000];
. . .
Arrays.sort(a)
~~~
```

This method uses a tuned version of the QuickSort algorithm that is claimed to be very efficient on most data sets. The Arrays class provides several other convenience methods for arrays that are included in the API notes at the end of this section.

The program in Listing 3.7 puts arrays to work. This program draws a random combination of numbers for a lottery game. For example, if you play a "choose 6 numbers from 49" lottery, the program might print this: