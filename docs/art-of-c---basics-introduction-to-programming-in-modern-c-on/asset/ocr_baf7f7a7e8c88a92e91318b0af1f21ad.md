The following program does simple math for you to answer these questions. The main logic of the program is all in the main "Program.cs" file:

birth-date/Program.cs

```
using Example;

} var smiley = char.ConvertFromUtf32(0x1F642);

5 while (true) {
Console.WriteLine("What is your birth date? (mm/dd/yyyy)");
var input = Console.ReadLine();

9 if (DateTime.TryParse(input, out DateTime date)) {
10 var weekday = BirthDate.Weekday(date);
Console.WriteLine($"You are a {weekday} child.");

13 var days = BirthDate.AgeInDays(date);
14 Console.WriteLine($"You are {days} days old as of today.");

var (hours, mins) = BirthDate.AgeInHours(date);
17 Console.WriteLine($"\u{1F642}You are {hours} hours
and {mins} minutes old as of right now. {smiley}");

20 break;
21 } else {
22 Console.WriteLine("Invalid date. Try again? Yes (Y) or No
(N)");

24 var ans = Console.ReadLine() ?? "";
var firstLetter = (ans.Length > 0) ? ans.Substring(0,
1).ToUpper() : "";
switch (firstLetter) {
case "Y":
28 continue;
29 case "N":
default:
Console.WriteLine($"Your loss! {smiley}");
```