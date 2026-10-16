
On top of that, we want the static keyword to be on the class, thus ensuring the entire class is a static class. To begin with, the basic class, no extension methods yet, would look like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ExtensionMethods
{
    public static class StringExtensions
    {
    }
}
```

We haven’t talked very much about static classes yet so I will just explain briefly about what it means. When a class is static, every method inside the class must also be static. That also means that instances of static classes cannot be made – imagine saying something like StringExtensions extensions = new StringExtensions();. You just can’t do it and while that might seem to be somewhat restrictive, it does mean that the compiler and .NET framework can handle things in a way that benefits performance.

Defining the extension method is simple – create a method as static and make the first parameter as the object type that we want the extension method for, i.e. string, and mark it using the ‘this’ keyword:

```
public static string ToRandomCase(this string text)
{
    // We will put the method implementation here shortly...
}
```

A return type can be indicated and, as well as the initial parameter that uses the ‘this’ keyword, we could add as many other parameters as we want.

As it was indexers and operator overloading, this is nothing more than syntactic sugar. The compiler will go ahead and change anywhere that the extension method is called into nothing more than calling a method (the extension in this case). When we have finished, we can simply say:

```
string title = "Hello World!"
string randomCaseTitle = title.ToRandomCase();
```

And the compiler will turn that into this:

```
string title = "HelloWorld";
string randomCaseTitle = StringExtensions.ToRandomCase(title);
```

What we end up with is a piece of code that looks better, is far easier to read, and looks like nothing more than a proper method for the string class.

But this isn’t all it seems to be. While the method will seem like it is part of the original string class, it isn’t. If your extension method isn’t in the same namespace as the original class, you could face a problem where your class is recognized but the extension method won’t be found, or you might move to another project only to find that what you saw as an original class method was actually an extension method that someone else wrote and now you can’t use it.

I’m not saying don’t use these extension methods. You should use them or I wouldn’t be telling you about them, but you just need to keep in mind that, while methods may look like part of a class, it might not be; it might be an extension method.

You might also need to have a using statement in the extension method, but that will be dependent on the namespace you used.

Let’s complete the code example by finishing the ToRandomCase method body:

```
string result = "";

for (int index = 0; index < text.Length; index++)
{
    if (random.Next(2) == 0)
    {
        result += text.Substring(index, 1).ToUpper();
    }
    else
    {
        result += text.Substring(index, 1).ToLower();
    }
}

return result;
```

One character at a time, this will go through our original string and pick a random number, which will be 0 or 1. For 0, the character is made upper case and for 1, the character is made lower case. That way, we end up with a collection of random upper and lower case letters which gives us the result we wanted.

The entire code should now look like this:

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ExtensionMethods
{
    public static class StringExtensions
    {
        private static Random random = new Random();

        public static string ToRandomCase(this string text)
        {
            string result = "";

            for (int index = 0; index < text.Length; index++)
            {
                if (random.Next(2) == 0)
                {
                    result += text.Substring(index, 1).ToUpper();
                }
                else
                {
                    result += text.Substring(index, 1).ToLower();
                }
            }

            return result;
        }
    }
}
```

As we said before, if your program knows there is an extension method, we can do this:

```
string message = "I'm so sorry, Simon.  I really can't do that.";
```

```
Console.WriteLine(message.ToRandomCase());
```

The extension method can be used as if it was part of our original class.

## Quick Primer

- Extension methods help us to create methods that seem as though they are part of a class, like the string class, when you can’t access the class to modify it, and then help us to add the method.
- You must add an extension method as a static method in a static class. The first parameter must be the type for the class you want the method added to and you must use the ‘this’ keyword, i.e. public static class StringExtensions { public static string ToRandomCase(this string text){ /* We put the method implementation here */} }.
- When you have created an extension method, it can be called just as if it were a proper part of the class: string text = “Hello World!”; randomCaseText = text.ToRandomCase();.
- An extension method is just a way of making your code look presentable and easier to read. Whatever you write, the compiler will rewrite it whenever the extension method is used to call the static method directly.

Well, that brings us to the end of this advanced section, but we are not finished, not by a long shot. First, we’ll take a break. I’ve given you some questions to answer in the next section (answers at the back of the book) and then we’ll move on to more advanced topics.

## Quick Quiz

1. Of the four choices below, which one is NOT allowed as an access modifier in C#?
   + a) public
   + b) friend
   + c) protected
   + d) internal

2. Look at the C# code and decide, from the choices, what [int i] is.

```
class MyClass
{
// ...

public string this[int i]
{
get{ return arr[i];}
set{ arr[i] = value; }
}
}
```

   + a) Property
   + b) Event
   + c) Indexer
   + d) Delegate

3. Look at the C# keywords below – which one is not associated with multithreading?
   + a) async
   + b) await
   + c) sealed
   + d) lock

4. In the C# Generics examples below, which is the invalid expression:
   a) class A where T : class, new()
   b) class A where T : struct, IComparable
   c) class A where T : Stream where U : IDisposable
   d) class A where T : class, struct

5. In C#, the new keyword is used to create new objects from a type. Which of these cannot make use of the new keyword:
   a) Interface : var a = new IComparable();
   b) Class: var a = new Class1();
   c) Struct : var a = new Struct1();
   d) C# object : var a = new object();

6. Look at the four examples below where button1 is used in WinForms as a Button Class object. Which one is an incorrect click event handler expression?
   a) button1.Click += (s, e) => MessageBox.Show("Click");
   b) button1.Click += delegate(EventArgs e)
   {MessageBox.Show("Click");};
   c) button1.Click += new System.EventHandler(button1_Click);
   d) button1.Click += delegate { MessageBox.Show("Click"); };

7. Look closely at the C# code below. Which of the using statements is incorrect?
   using System; // 1.
   namespace Co
   {
       using System.Text; // 2.
       namespace App
       {

```
using System.IO; // 3.
class Class1
{
using System.Text; // 4.
static void A()
{
}
}
}
}
```

   + a) 1
   + b) 2
   + c) 3
   + d) 4

8. Look at the following C# code – what will the output be?

```
int? i = 8 >> 5;
int? j = i > 0 ? i : null;
var a = j ?? int.MinValue;
Console.WriteLine(a);
```

   + a) 1
   + b) Null
   + c) 0
   + d) -2147483648

9. Which of the following statements regarding C# exceptions is correct:
   + a) C# exceptions occur at linking time
   + b) C# exceptions occur at compile time
