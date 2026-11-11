```
public void swap(int a, int b) {
    int temp;
    temp = a; /* saving the value of a */
    a = b;   /* putting b into a */
    b = temp; /* putting temp into b */
}
static void Main(string[] args) {
    NumberChecker n = new NumberChecker();

    /* defining a local variable */
    int x = 10;
    int y = 20;

    Console.WriteLine("Before swapping, value of x is : {0}", x);
    Console.WriteLine("Before swapping, value of y is : {0}", y);

    /* let’s swap the values by calling the function */
    n.swap(x, y);

    Console.WriteLine("After swapping, value of x is : {0}", x);
    Console.WriteLine("After swapping, value of y is : {0}", y);

    Console.ReadLine();
}
}
}

```

The code gives the following output: