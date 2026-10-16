```
score = value;
}
}
```

Here, anyone can use the getter but the setter can only be accessed from within the class it is in.

# Auto-Implemented Properties

You will also find yourself creating quite a lot that looks like this:

```
private int score;
```

```
public int Score
{
    get
    {
        return score;
    }
    set
    {
        score = value;
    }
}
```

With C# v3.0, a new feature was introduced which allows the ability to make auto-implemented properties that do the same things. Instead of using that code above and that includes our private instance variable called score, you would just do this:

```
public int Score { get; set; }
```

Behind the scene, a default instance variable is created along with the basic code for get and set. What you won’t have is access to the