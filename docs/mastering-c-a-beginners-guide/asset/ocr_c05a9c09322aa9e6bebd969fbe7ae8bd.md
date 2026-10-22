```
Console.WriteLine("The fake answer to life: " + SomeClass.TheFakeAnswerToLife);
Console.WriteLine("The real answer to life: " + SomeClass.GetAnswer());
}
}
class SomeClass
{
private const int TheAnswerToLife = 42;
public const int TheFakeAnswerToLife = 43;

public static int GetAnswer()
{
return TheAnswerToLife;
}
}
}
```

Notice how I define a class (SomeClass) with two constants. The first is private, so it can only be accessed from the class itself, but the other is public. So, in our main program code, I access both constants differently—first directly, since the fake answer is publicly available, and secondly with the help of the GetAnswer() method.

# Which Types Can Be Used as a Constant?

Since constants have to be declared immediately and can’t be changed later on, the value you assign to a constant has to be a constant expression. The compiler must evaluate the value already at compile time. This means that numbers, Boolean values, and strings can be used just fine for