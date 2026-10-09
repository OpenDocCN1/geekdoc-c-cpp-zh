![](bbox=[0.18, 0.17, 0.82, 0.53])

The sample code of this lesson is based on the information from the official Mega Millions website, www.megamillions.com, in particular, from this page, How to Play [https://www.megamillions.com/How-to-Play.aspx].

# 15.2. Code Reading - Lottery Simulation

The main program is rather simple. All the game logic is implemented in the static method `Millions.Play()` in the namespace `Mega`.

`mega-millions/Program.cs`

```
```csharp
Console.WriteLine($"Let's play Fake Mega Millions (for fun)!");
Mega.Millions.Play();
```
```