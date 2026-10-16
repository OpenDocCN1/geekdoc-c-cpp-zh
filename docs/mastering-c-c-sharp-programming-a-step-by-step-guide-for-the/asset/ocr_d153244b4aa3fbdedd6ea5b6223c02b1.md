We’ll start by creating a class. This is a template, a blueprint if you like, for all objects of the specified type, and it will say what the object can do and what it can store. Rather than diving straight into this subject and creating classes and objects, we’ll start by playing with some that are already created as part of the .NET framework.

# Creating an Object

Let’s begin by using the class called Random. This is a great class that lets you create some random numbers. This class can be used for all sorts of things – determining what a die roll will be, shuffling a card deck, even making some random things happen.

There is one thing I need to say about generating random numbers – in general, on a computer a random number isn’t actually random; they are called “pseudo-random”. These numbers are picked using an algorithm that makes them look random. The programmer needs to choose a starting number to get things started and this number is known as a ‘seed’. Start with the same seed each time and you will get the same random number sequence each time.

To stop this, the random number generator may be seeded with the current time, right down to the millisecond – that way, the game will play out differently every time.

We’re going to use the Random class and this will automatically seed the algorithm with the current time – although you do have the option of specifying the seed if you want.

The process of creating objects is much like that of creating a variable. We use the following:

```
Random random = new Random();
```

The first thing we do is specify what type the variable will be. However, unlike the variable where we used types such as int, char, string, etc., this time we use the Random type which is also the Random class.

Next, the variable is named – we’ve called it random but you can call it whatever you want. It is common to name variables after the type.