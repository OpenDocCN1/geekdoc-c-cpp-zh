# ### 4.3. Code Reading - Hello World 4 Redux

```
hello-universe-4/Program.cs

class Program {
    static void Main() => Console.WriteLine(
        string.Format("Hello {0}! How are you?", ReadName())
    );

    static string? ReadName() {
        Console.WriteLine("What is your name?");
        var name = Console.ReadLine();

        if (string.IsNullOrEmpty(name)) {
            name = "Friend";
        } else {
            name = name.ToUpper();
        }

        return name;
    }
}

```

This example code is semantically equivalent to "hello-world-4".

> Is this "Hello World" thing ever gonna end? ☺

This is the last one. It's a promise! ☺ But, remember, it is not about "hello world" or any particular examples that we use in this book. We are learning the C# language, and its idiomatic modern programming styles. Note that the book begins rather slow, but it quickly starts to progress pretty fast. Better fasten your seatbelt! ☺

# #### 4.3.1. Explanation

This program behaves in exactly the same way as its earlier counterpart, hello-world-4. The program asks the user for his/her name as before, and it uses the user