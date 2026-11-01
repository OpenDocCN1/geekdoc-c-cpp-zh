# EXERCISES

13.1. Write the code for an event handler that uses the general-purpose (object sender, EventArgs e) syntax that will accept either the Timer.Elapsed event or the Connection.MessageArrived event from the code shown earlier in this chapter. The handler should output a string specifying which type of event has been received, along with the Message property of the MessageArrivedEventArgs parameter or the SignalTime property of the ElapsedEventArgs parameter, depending on which event occurs.

13.2. Modify the card game example to check for the more interesting winning condition of the popular card game, rummy. This means that a player wins the game if his or her hand contains two "sets" of cards, one of which consists of three cards and one of which consists of four cards. A set is defined as either a sequence of cards of the same suit (such as 3H, 4H, 5H, 6H) or several cards of the same rank (such as 2H, 2D, 2S).

13.3. Why can't you use an object initializer with the following class? After modifying this class to enable the use of an object initializer, give an example of the code you would use to instantiate and initialize this class in one step:

```
```csharp
public class Giraffe
{
    public Giraffe(double neckLength, string name)
    {
        NeckLength = neckLength;
        Name = name;
    }
    public double NeckLength {get; set;}
    public string Name {get; set;}
}
```
```

13.4. True or false: If you declare a variable of type var, you will then be able to use it to hold any object type.

13.5. When you use anonymous types, how can you compare two instances to determine whether they contain the same data?

13.6. Try to correct the following code for an extension method, which contains an error:

```
```csharp
public string ToAcronym(this string inputString)
{
    inputString = inputString.Trim();
    if (inputString == "")
    {
        return "";
    }
    string[] inputStringAsArray = inputString.Split(' ');
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < inputStringAsArray.Length; i++)
    {
        if (inputStringAsArray[i].Length > 0)
        {
            sb.AppendFormat("{0}",
                inputStringAsArray[i].Substring(
                0, 1).ToUpper());
        }
    }
```
```