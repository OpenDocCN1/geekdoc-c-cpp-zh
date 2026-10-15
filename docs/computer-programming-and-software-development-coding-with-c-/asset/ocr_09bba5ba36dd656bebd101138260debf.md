strings. So you see me using here a double equals sign. This operation will return a Boolean, and you may already guess that the result of this will be false. So what I did here was an equality check, and C# will do a comparison, and it will also take into account, by default, whether or not that character is lowercase or uppercase. So in this case, these two strings are not equal then. If I'm going to check if name1 is equal to another string Bethany, and let's put this one in comment, the result is indeed True. So although I'm comparing two different strings, they are equal. In this case, I'm now checking if name2 is equal to uppercase Bethany. But in this case, I'm not using the double equals sign; I'm using the .Equals met.

```
//Console.WriteLine("Are both names equal? " + (name1 == name2));
//Console.WriteLine("Is name equal to Bethany? " + (name1 == "Bethany"));
//Console.WriteLine("Is name equal to BETHANY? " + name2.Equals("BETHANY"));
Console.WriteLine("Is lower name equal to bethany? " + (name1.ToLower() == "bethany"));

Console.ReadLine();
```

The result is the same indeed because the double equals sign, as well as the .Equals method do the same thing. If I want to do a case insensitive comparison, I can again bring in the ToLower or ToUpper. In that case, I just do a ToLower or ToUpper on both sides, and then I actually can compare without taking into account the casing. And in this case, I'm going to check if they want ToLower is equal to bethany, also lowercase. And that's, , going to result in True. Say that we have a string that contains the word Hello. I then create a new string, b, and I set it to a on the next line. Then in the next line, I'm adding to b using +=, space, world. Then, we asked to see what a is.