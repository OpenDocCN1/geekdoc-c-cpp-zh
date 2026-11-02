# Postincrement

```
System.out.println( gumballs++ );
```

... and, by the way, add 1 to gumballs, changing the value of gumballs from 28 to 29.

# Preincrement

```
System.out.println( ++gumballs );
```

... and, by the way, add 1 to gumballs, changing the value of gumballs from 28 to 29.

If you don't use Eclipse, you may see a different error message:

```
unexpected type
required: variable
found   : value
gumballs++++;
```

Eclipse or no Eclipse, the bottom line is the same: Namely, your code contains an error, and you have to fix it.

So how can you add values other than 1? As luck would have it, Java has plenty of assignment operators you can use. With an assignment operator, you can add, subtract, multiply, or divide by anything you want. You can do other cool operations, too.

For example, you can add 1 to the kids variable by writing

```
kids += 1;
```

Is this better than kids++ or kids = kids + 1? No, it's not better. It's just an alternative. But you can add 5 to the kids variable by writing

```
kids += 5;
```

You can't easily add 5 with preincrement or postincrement. And what if the kids get stuck in an evil scientist's cloning machine? The statement