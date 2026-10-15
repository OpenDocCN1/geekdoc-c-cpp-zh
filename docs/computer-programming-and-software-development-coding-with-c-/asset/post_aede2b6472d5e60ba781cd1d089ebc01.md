
also a thing called parsing. Now parsing allows us to take a string value and convert it, or should I say parse it, to another type. It's a very common thing to do, but it's more related to strings, and thus we'll take a look at it in the next chapter.

## Chapter 5 Implicit Typing Fundamentals

Now, I want to briefly discuss one more thing related to types, and it's implicit typing. I have already mentioned a few times that once a type is set for a variable, it's done, it's set, and so far we have been explicit about this, meaning that we included the type name, so int or bool, in its declaration. That is the normal way of doing things in C#.

```
int a = 123;

bool b = true;

double d = 11.0;
```

Since C# 3, so already for quite a few versions, C# supports implicit typing. As the name gives away, implicit typing allows us to ask C# to figure out itself based on what is on the side of the equal sign what the type will be. We use for that the var keyword, basically saying, hey C#, here's a variable, please figure out the type yourself. Take a look here. I have here var a = 123. 123 is an integer value, and thus C# will create a to be of type integer. If we do var b = true, C# will understand that true is a Boolean value and thus b will be of type bool. You may be thinking, is C# then allowing us to omit the type?

```
var a = 123;//a will be an integer
var b = true;//b will be a boolean
var d = 11.0;//d will be a double
```

Well, that's a great question, and the answer is it's not. It's still creating the variable with the data type it finds. The data type is decided on upon compile time, so it's known what our a, b, and d will be here before the application runs. Just like before, we also can't change the type later on. The types are still set. Using var means that the type is inferred. C# will look at the expression on the side, and based on the result of that it will know what the type of the variable will be. You can pretty much everywhere, where we have used so far our explicit typing, use implicit typing, although there are some exceptions. However, it can lower the readability of your code since it's harder to understand what type a variable will be; however, and this goes beyond the scope of this book, there are places in C# where implicit typing is pretty much the only way forward. When you learn about LINQ later in this path, you'll see that in quite a few cases the use of var is required. Let us return one more time to Visual Studio and see how we can use var. So far, we have done what we typically would do. We specified type, then we specified the name of the variable, and optionally assigned a value. But, in C# we can also use implicit typing. Instead of writing the type, I can also use var here instead. The var keyword is actually usable wherever I define a variable, such as an integer value, it could be that I replace bool with it or I could also replace this double with it. What I've done here is I've used implicit typing. This can actually be used to let C# figure out the type. So instead of me explicitly specifying the type, I let C# figure it out by looking at the side. That means that if I hover over this monthlyWage, it still knows which type it is going to be because C# looked at what was on the side of the assignment operator. That's the same for this isActive and the same for this rating here as well. So by using var, I have

now all of a sudden made it possible that I change the type. I can still not say that all of a sudden monthlyWage is now a Boolean in the next line. That still doesn't work because of type safety.

```
class Program
{
    static void Main(string[] args)
    {
        var monthlyWage = 1234;
        int months = 12, bonus = 1000;

        var isActive = true;
        var rating = 99.25;

        //monthlyWage = true;

        double ratePerHour = 12.34;
        int numberOfHoursWorked = 165;

        long veryLongMonth = numberOfHoursWorked;
        double d = 123456789.0;
        int x = (int)d;

        int intVeryLongMonth = (int)veryLongMonth;

        double currentMonthWage = ratePerHour * numberOfHoursWorked + bonus;

        //Console.WriteLine(currentMonthWage);

        ratePerHour += 3;//ratePerHour = ratePerHour + 3;

        if (currentMonthWage > 2000)
```

You may be thinking is this really worth it? Well it is, in my opinion, often a personal preference. Some people actually like always writing var, some people, including me, actually like to be more explicit. I typically tend to always specify the type when creating a variable. It makes the code a little bit more readable, but it is personal preference. There are cases in C#, though, where we actually cannot at compile know the type, and then you will always have to use implicit typing. Let's summarize what you have seen. Probably the most single important lesson here is that C# is a strongly typed language. C# will guard that types are respected. Some other

languages don't do this, it's definitely a plus when using C#. We have in this chapter looked mostly at using primitive data types, which are value types. For these primitive data types, C# comes with a number of keywords, such as int and bool. We've then also looked at the different options we have to convert data from one type to the other, and we've seen what different options exist for this. In the next chapter, we'll look at another very important data type, and that is strings.

## Chapter 6 How to Create and Use Strings

Text, the written word, what would we be without it? On average, we see many thousands of words on a daily basis, in the newspaper, on our phone, on the bus that drives by, and also in applications. Words and written text are very common. It's quite understandable that a major programming language such as C# also has a lot on board to help us work effectively in our applications with text. First, we need to get to know the string type a bit since it is, well, different to what we've seen so far. Once we have gone through this short introduction, then we'll start working with strings. As said, strings behave differently, and they will even amaze you at times. One of the interesting things about them in C# is that they are immutable. I'll explain what this means and why this is important for you as a C# developer to take this into account. Finally, as promised in the previous chapter, we'll take a look at how we can convert, or I should say parse, a snippet of text into another type. And let's dive in by taking a look in some more detail at strings and their specifics in C#. A string in C# consists out of a series of characters, chars really. Think of it as an array of characters. Together, they represent a piece of text. This can be a short text, even just a space or an empty string, or contain an entire book. When creating a string, as you'll see in a minute, the actual text is always surrounded with double quotes. This is different from a char, which we looked at in the previous chapter, which had single quotes. When creating a string in C#, the type that we get is the string, and you'll typically use the lowercase keyword as type to create a string. Just like we

already saw, the actual type is String, so with the capital. Lowercase string is, again, just an alias for the type, so the one with the uppercase. In this chapter, we'll take a look at using the many methods provided by the string type. You may remember from the previous chapter that C# has value types and reference types. The types we looked at in the previous chapter were indeed value types. Strings, however, are different as they are stored on the heap and thus are reference types really. However, most of the behavior of the string type is actually similar to a primitive type, as you'll see soon.

```
string s1 = "Hello world";
string s2 = string.Empty;
var s3 = "I am a string too!";
string s4 = null;
string s5;
```

We'll explore later in the book in more detail what being a reference type really means in terms of the behavior of the string type. You can see I'm declaring a couple of strings. In the first line, I have used the string type, and I've created a string named s1, and I've initialized it with probably the most commonly used phrase in computer history, Hello world. Notice that the string is surrounded with double quotes, which indicates the start and the end of the string. A string can be empty. We could create a string using a pair of double quotes with really no content between them. That's an empty string. But as said, the string type contains many methods to enable us to work easily with strings, and one of these helper methods is string.Empty. This will create a new empty string and
