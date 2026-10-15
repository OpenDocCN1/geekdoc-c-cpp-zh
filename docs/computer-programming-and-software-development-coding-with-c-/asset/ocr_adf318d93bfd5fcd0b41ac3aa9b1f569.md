You have different refactorings available in different contexts, and some go way beyond inlining a variable. You can ask Visual Studio to bend and twist your code in so many ways. For example, this string concatenation. It's a bit of an eyesore with all these snippets of string joined together.

![](bbox=[0.121, 0.269, 0.914, 0.309])

C# has a more elegant way to combine strings called string interpolation. And if you open the refactoring menu, Visual Studio offers to convert this concatenation to an interpolated string, so let's do it.

![](bbox=[0.121, 0.525, 0.914, 0.577])

This $ prefix means that this is an interpolated string, which means it contains snippets of code in curly braces. So C# evaluates these snippets, it evaluates this variable, and calls this method and embeds the results in the string. Nicer code, more readable, and we did not have to write it by hand. Visual Studio did it for us. We improved this class. It's certainly not perfect yet. For example, one confusing details is that ComfortIndex() takes the temperature in degrees Fahrenheit, while a Report() takes it in Celsius and then converts it to Fahrenheit before calling ComfortIndex(). So, this code is more convoluted than it could be. Now we have two files in our project. One contains the WeatherUtilities class, and the other contains the