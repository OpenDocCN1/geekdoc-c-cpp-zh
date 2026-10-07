```
const int command = 0;
const int fileName = 1;
const string dataFile = "data.dat";

// ...
if ((args.Length, args[command].ToLower()) is (1, "cat")
{
    Console.WriteLine(File.ReadAllText(dataFile));
}
else if ((args.Length, args[command].ToLower()) is (2, "encrypt")
{
    string data = File.ReadAllText(dataFile);
    File.WriteAllText(
        args[fileName], Encrypt(data).ToString());
}
```

As expected, the same is possible with the switch expression or statement syntax
see Listing 7.28

# Listing 7.28: Tuple Pattern Matching with the switch Statement

```
public static void Main(params string[] args)
{
    const int action = 0;
    const int fileName = 1;
    const string dataFile = "data.dat";

    // ...
    switch ((args.Length, args[action].ToLower())))
    {
        case (1, "cat"):
            Console.WriteLine(File.ReadAllText(dataFile));
            break;
        case (2, "encrypt"):
            {
                string data = File.ReadAllText(dataFile);
                File.WriteAllText(
                    args[fileName], Encrypt(data).ToString());
            }
            break;
        default:
            Console.WriteLine("Arguments are invalid.");
            break;
    }
```