```
    // Indicate true if passed either exit or quit,
    // irrespective of case.
    if (String.Compare("exit", source, true) == 0) ||
        (String.Compare("quit", source, true) == 0)
    {
        quitting = true;
    }
```

This version is simpler than the previous looping version. This code doesn't need to worry about case, and it can use a single conditional expression because it now has only two options to consider instead of a longer list: any spelling variation of QUIT or EXIT.

# ## What If I Want to Switch Case?

You may be interested in whether all of the characters (or just one) in a string are uppercase or lowercase characters. And you may need to convert from one to the other.

# ### Distinguishing between all-uppercase and all-lowercase strings

I almost hate to bring it up, but you can use the switch command (see Chapter 5 of this minibook) to look for a particular string. Normally, you use the switch command to compare a counting number to some set of possible values; however, switch does work on string objects, as well. This version of the termination section in BuildASentence uses the switch construct:

```
    switch(line)
    {
        case "EXIT":
        case "exit":
        case "QUIT":
        case "quit":
            return true;
    }
    return false;
```

This approach works because you're comparing only a limited number of strings. The for loop offers a much more flexible approach for searching for string values. Using the case-less Compare() in the previous section gives the program greater flexibility in understanding the user.

# ### Converting a string to upper- or lowercase

Suppose you have a string in lowercase and need to convert it to uppercase. You can use the ToUpper() method: