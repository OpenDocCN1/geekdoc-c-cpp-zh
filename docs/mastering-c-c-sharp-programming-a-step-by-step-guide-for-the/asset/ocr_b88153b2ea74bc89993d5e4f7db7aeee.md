```
numbers = new int[0];
}

public AddNumber(int newNumber)
{
    // Add code here to make a new, slightly bigger, array,
    // bigger than it was before, and then add in your number.
}

public object GetNumber(int index)
{
    return numbers[index];
}
}
```

This is by no means finished but, hopefully, you get the gist of it. You simply create your class and you use that int type liberally.

Ok, but what if you now want a list of strings? It’s sad that you can’t use all that hard work, isn’t it? You can’t use your ListOfNumbers class and add strings to it so what do we do now? Think about it. Got any ideas?

We could probably make another class, similar, and name it ListOfStrings, couldn’t we? It would look much the same as our ListOfNumbers class but it would have the string type and not the int type.

To be fair, you could go a little bit mad here and make all kinds of ListOf classes, one for each type. But wouldn’t you find that irritating? You would have an almost unlimited number of these classes.