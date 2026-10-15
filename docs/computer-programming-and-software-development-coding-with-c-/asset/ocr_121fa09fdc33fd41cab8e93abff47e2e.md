```
```csharp
int intMaxValue = int.MaxValue;
int intMinValue = Int32.MinValue;

char userSelection = 'a';
char upperVersion = char.ToUpper(userSelection);
bool isDigit = char.IsDigit(userSelection);
bool isLetter = char.IsLetter(userSelection);

DateTime hireDate = new DateTime(2021, 3, 28, 14, 30, 0);

Console.WriteLine(hireDate);

DateTime exitDate = new DateTime(2021, 12, 11);

Console.ReadLine();
```
```

In Visual Studio, I can see a number of options, those are overloads. Again, we'll come to that. And these are combinations of parameters I can use to create my new DateTime. So let's create a DateTime in the year 2021, then I write a comma, then the month, let's take March, and let's take as the date the 28th. I can leave the hour and minute and the second out. I can also set them to a value or I can also set them to 0, and that would mean midnight, but let us here select half past 2, so that would be 14 hours, 30 minutes, and hiring is not to the second, so we'll leave that to 0. So now I've created my first DateTime. I can also ask C# to write that DateTime to the console.

![](bbox=[0.12, 0.737, 0.429, 0.77])

And let's see what that does. And there we go, we see the date, the 28th of March of 2021 at half past 2. This is Europe notation. This will depend on your regional settings how this date is being displayed here. Now as you can see, there are other options to