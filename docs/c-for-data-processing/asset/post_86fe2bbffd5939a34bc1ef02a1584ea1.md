
```csharp
;
```

The semicolon marks the end of the list of variable names, and also the end of that declaration statement. All statements in C# programs are separated by the ; character, this helps to keep the compiler on the right track.

The ; character is actually very important. It tells the compiler where a given statement ends. If the compiler does not find one of these where it expects to see one it will produce an error. You can equate these characters with the sprocket holes in film, they keep everything synchronised.

```csharp
string widthString, heightString;
```

We have made some variables which can hold numbers. Now we are going to make some which can contain strings. This is because when we read the numbers from our user we first read them in as strings of text. We then convert the text into a number. The variables widthString and heightString (note the sensible names) will contain text versions of the numbers.

```csharp
widthString =
```

This is an assignment statement. In this C# statement we are going to change the value in a variable. Our program is going to read a line of text from the user and place the result in the variable we have called widthString. Remember that a variable is simply a named box of a particular size, which can hold a single data item (in this case a string of text).

A good proportion of your programs will be instructions to assign new values to variables, as the various results are calculated. C# uses the = character to make assignments happen. The first part of this statement is the name of a previously defined variable. This is followed by the = character which I call the gozinta. I call that because the value on the right gozinta (goes into) the variable on the left. Sorry.

### Console.

On the right of the equals we have the thing which is going to be assigned to widthString. In this case the result is going to be the string returned by the method ReadLine. This method is part of an object called Console which looks after the user input and output. The full stop (.) separates the object identifier from the method identifier.

### ReadLine

This indicates that the ReadLine method is to be invoked. This asks the running program to dash off, do whatever statements there are in this method, and then come back. Methods are a way in which you can break up your program into a number of chunks, each of which has a particular job. They also mean that you only have to write a particular piece of code once, put it in a method, and then call that method whenever you want that particular job done. The C# system contains a number of built-in methods to do things for our programs. ReadLine is one of these.

When this program runs the ReadLine method is invoked (or called). It will wait for the user to enter a line of text and press the Enter key. Whatever is typed in is then returned as a string by the ReadLine method. The result of the method call is placed in the widthString variable.

### ()

A method call is followed by the parameters to the method. A parameter is something that is passed into a method for it to work on. Think of it as raw materials for a process of some kind. In the case of ReadLine it has no raw materials; it is going to fetch the information from the user who will type it in. However, we still have to provide the list of parameters even if it is empty.

### ;

We have seen the semi-colon before. It marks the end of a statement in our program.

### width =

This is another assignment (Mr. Phelps/Hawke¹). The variable width is being given a value. Many statements in your programs will simply be moving data around and performing actions on it.

### double.

But the rest of the statement looks a bit scary. In fact it is not too tricky. We are asking Mr. double (the thing responsible for holding double precision floating point numbers) to do a little job for us. In this case the little job is "take the string held by widthString and convert it into a double precision floating point number." Mr. double provides this ability by exposing a method called Parse.

Note that there is nothing wrong or naughty about something in C# exposing its methods. It is how we get things done for us. When you come to design larger programs you will find that the best way to do this is to create components which expose methods to get the job done. The whole of the C# library set is provided as a series of methods and one of the things that you will have to get to grips with is where the methods are and how to use them. As with many things in life, the trick is knowing who to ask...

### Parse

The Parse method has the job of converting the string it has been given into a double precision floating point number. To do this it must look along the string, pull out each digit in turn and then calculate the actual value, as in "12" means a ten and two units. This process of looking along things is often called parsing. Hence the name of the method we are using. The method is given the string that is to be parsed and returns the number that it has found.

Note that this gives significant potential for evil, in that if the user doesn't type in a value or types something like "Twenty Five" the Parse method call will not be able to resolve a number and will fail as a result. How it fails, and how you can resolve this failure, will be left for a future section in order to add more excitement to this text.

### (widthString);

We have seen that a call of a method must be followed by the raw materials (parameters) for that method. In the case of ReadLine there are no parameters, but we still need to supply an empty list to indicate this. In the case of Parse the method needs to be given the string that it is to work on. We do this by putting the name of the string variable containing the text (widthString) into the brackets as above. The value of the information in widthString (i.e. the text that the user has typed in) is passed into the Parse method for it to work on and extract the number from.

¹ Obscure movie/TV show reference for you there folks.

```csharp
heightString = Console.ReadLine();
height = double.Parse(heightString);
```

These two statements simply repeat the process of reading in the text of the height value and then converting it into a double precision value holding the height of the window.

```csharp
woodLength = 2*(width + height)*3.25;
```

When I write programs I use brackets even when the compiler does not need them. This makes the program clearer.

This is the actual nub of the program itself. This is the bit that does the work. It takes the height and width values and uses them to calculate the length of wood required.

The calculation is an expression much like above, this time it is important that you notice the use of parenthesis to modify the order in which values are calculated in the expression. Normally C# will work out expressions in the way you would expect, i.e. all multiplication and division will be done first, followed by addition and subtraction. In the above expression I wanted to do some parts first, so I did what you would do in mathematics, I put brackets around the parts to be done first.

Note that I use a factor of 3.25 to allow for the fact that the customer wants the length of wood in feet. There are around 3.25 feet in a meter, so I multiply the result in meters by this factor.

The + and * characters in the expression are called *operators* in that they cause an operation to take place. The other items in the expression are called *operands*. These are what the operators work on.

```csharp
glassArea = 2 * (width * height);
```

This line repeats the calculation for the area of the glass. Note that the area is given in square meters, so no conversion is required. I've put one multiplication in brackets to allow me to indicate that I am working out two times the area (i.e. for two panes of glass). There is no need to do this particularly, but I think it makes it slightly clearer.

```csharp
Console.WriteLine
```

This is a call of a method, just like the ReadLine method, except that this one takes what it is given and then prints it out on the console.

```csharp
(
```

This is the start of the *parameters* for this method call. We have seen these used in the calls of Parse and also ReadLine.

```csharp
"The length of the wood is "
```

This is a *string literal*. It is a string of text which is literally just in the program. The string of text is enclosed in double quote characters to tell the compiler that this is part of a value in the program, not instructions to the compiler itself.

```csharp
+
```

Plus is an addition operator. We have seen it applied to add two integers together. However, the plus here means something completely different. In this case it means "add two strings together".
