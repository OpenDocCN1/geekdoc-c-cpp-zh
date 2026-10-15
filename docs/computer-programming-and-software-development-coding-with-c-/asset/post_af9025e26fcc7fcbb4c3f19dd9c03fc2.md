
strings. So you see me using here a double equals sign. This operation will return a Boolean, and you may already guess that the result of this will be false. So what I did here was an equality check, and C# will do a comparison, and it will also take into account, by default, whether or not that character is lowercase or uppercase. So in this case, these two strings are not equal then. If I'm going to check if name1 is equal to another string Bethany, and let's put this one in comment, the result is indeed True. So although I'm comparing two different strings, they are equal. In this case, I'm now checking if name2 is equal to uppercase Bethany. But in this case, I'm not using the double equals sign; I'm using the .Equals method.

```
//Console.WriteLine("Are both names equal? " + (name1 == name2));
//Console.WriteLine("Is name equal to Bethany? " + (name1 == "Bethany"));
//Console.WriteLine("Is name equal to BETHANY? " + name2.Equals("BETHANY"));
Console.WriteLine("Is lower name equal to bethany? " + (name1.ToLower() == "bethany"));

Console.ReadLine();
```

The result is the same indeed because the double equals sign, as well as the .Equals method do the same thing. If I want to do a case insensitive comparison, I can again bring in the ToLower or ToUpper. In that case, I just do a ToLower or ToUpper on both sides, and then I actually can compare without taking into account the casing. And in this case, I'm going to check if name1.ToLower() is equal to bethany, also lowercase. And that's going to result in True. Say that we have a string that contains the word Hello. I then create a new string, b, and I set it to a on the next line. Then in the next line, I'm adding to b using +=, space, world. Then, we ask to see what a is.

Take a look at the snippet you see here on the screenshot. I'm creating a new StringBuilder. Don't worry about this new thing here. That's the constructor again, and we'll learn about it later. Then, on my StringBuilder, I'm calling the Append method to append the string. I'm doing it a few times using AppendLine, which will append the string I'm passing in on a new line. Using the StringBuilder, none of this will result in the string being copied over multiple times, which would be the case for regular strings. Finally, I can ask the StringBuilder to give me back, well, the actual string value, and so we can do that using the ToString method on our StringBuilder class.

## Chapter 8 Strings are Immutable

Time to head back to Visual Studio and make sure we understand string immutability and the StringBuilder. So far, we have been using strings, and without knowing, we've actually already come across string immutability. Because all these methods that we've used so far, like ToLower, they actually don't work on the original string. They return a copy of the original string. Well, let me show you that strings are immutable, and that whatever we do, we are working on a different string. Let's say that I create a string name again, and I set that equal to Bethany. I create another variable, let's call it anotherName, and I set that equal to name. So now I have two variables, name and anotherName, and they're both pointing to a string, Bethany.

```csharp
class Program
{
    static void Main(string[] args)
    {
        string name = "Bethany";
        string anotherName = name;

        Console.ReadLine();
    }
}
```

Strings are reference types. I don't expect you to already fully understand reference types, but it actually means that the string Bethany is stored somewhere on the heap, so in the main memory. And I have two "pointers" that point towards that string, name and anotherName. And if I say that to my name string, attach another string, and I'm going to use this increment operator here, which is going to extend the original string with, in this case, let's say Smith. Let's put a space in front of that. What I've done is I've actually created another string Smith, and I've attached that to Bethany, but I've not attached it to the original name string. No, in fact, a new string was created, and name is now pointing at a newly created string. Let's take a look at the output if I now write name and anotherName to the console. Let's see what happens.

![](img/0155736aec718cf18821e9f10a5d308d_688_0.png)

Name is now pointing to the concatenated string, Bethany Smith, but anotherName still says it's just Bethany. That is correct. Since I had set anotherName equal to name, and that means that they were originally pointing both to Bethany. The name variable has changed. It's pointing to the concatenated new string, but anotherName still points to the original string, Bethany, which was left untouched. The string immutability is something that will always happen as well. If I, for example, say that I want to have the lowercase name, and I say, well, take name and do it ToLower, now this is not going to touch the original string, it's going to return us a copy of the original string with every character converted to its lowercase counterpart. The original string, name, is left untouched. We're always getting back a copy. Because of this string immutability, some operations will actually result in a lot of strings being created, and that can actually be bad for memory consumption in our application. Say that I have this very simple loop here in which I'm going to loop 2500 times. I'm going to always concatenate to indexes, which is originally an empty string, the value of i. Now, by doing this this way, we're going to create 2500 copies of that string. Every time we attach to the original string, we're going to get back a new string. The original string is left untouched every time.

```csharp
name += " Smith";

Console.WriteLine("Name: " + name);
Console.WriteLine("Another name: " + anotherName);

string lowerCaseName = name.ToLower();

string indexes = string.Empty;
for (int i = 0; i < 2500; i++)
{
    indexes += i.ToString();
}

Console.ReadLine();
```

While I say that this can actually use more memory, don't start panicking. This is actually still the typical way of working with strings. But if you have to do a lot of concatenation within your application, say, for example, in a loop, using StringBuilder could actually be beneficial. Let's use the StringBuilder. I'm going to create a new StringBuilder. And when you start typing the word StringBuilder, you will actually see that Visual Studio gives you a word squiggly. It doesn't know about StringBuilder. That is because it lives in a different namespace and you have to bring that in. You can actually hover over StringBuilder, and then Visual Studio will give you some help, and it says you should actually bring in a namespace called System.Text. Well, let's agree for now, and we'll talk about version. Let's take a look at the result, and let's comment out these lines here. And now we indeed see that everything is on one line.

```csharp
26  string firstName = "Bethany";
27  string lastName = "Smith";
28
29  StringBuilder builder = new StringBuilder();
30
31  builder.Append("Last name: ");
32  builder.Append(lastName);
33  builder.Append("First name: ");
34  builder.Append(firstName);
35  string result = builder.ToString();
36
37  Console.ReadLine();
38
39  }
40 }
41
```

That's because I've used append. I should have actually used AppendLine, and this will include a line break at the end. We looked at converting from one type to another. Now with strings, we can actually do more, and we can actually parse a string value into another type. Let's take a look. Say that we allow the user to enter a value for the wage of an employee using our console application. The captured value will always be, indeed, a string.

```csharp
string w = Console.ReadLine();

double wage = double.Parse(w);

bool active = bool.Parse("true");
```

And we'll probably want to do some calculations with that entered value, and so we need to create, perhaps, a double from the entered value. So we need to convert it from a string to a double. We're going to parse the string into a double here, and this we can do using the Parse method on double. If the value can be parsed and it
