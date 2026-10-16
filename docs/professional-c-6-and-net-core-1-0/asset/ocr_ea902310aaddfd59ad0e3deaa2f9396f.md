```
foreach (var title in titles.Reverse())
{
    WriteLine(title);
}
WriteLine();
WriteLine("subset");
foreach (var title in titles.Subset(2, 2))
{
    WriteLine(title);
}
```

# Returning Enumerators with Yield Return

With the yield statement you can also do more complex things, such as return an enumerator from yield return. Using the following Tic-Tac-Toe game as an example, players alternate putting a cross or a circle in one of nine fields. These moves are simulated by the GameMoves class. The methods Cross and Circle are the iterator blocks for creating iterator types. The variables cross and circle are set to Cross and Circle inside the constructor of the GameMoves class. By setting these fields, the methods are not invoked, but they are set to the iterator types that are defined with the iterator blocks. Within the Cross iterator block, information about the move is written to the console and the move number is incremented. If the move number is higher than 8, the iteration ends with yield break; otherwise, the enumerator object of the circle yield type is returned with each iteration. The Circle iterator block is very similar to the Cross iterator block; it just returns the cross iterator type with each iteration (code file YieldSample/GameMoves.cs):

```
public class GameMoves
{
    private IEnumerator _cross;
    private IEnumerator _circle;

    public GameMoves()
    {
        _cross = Cross();
        _circle = Circle();
    }

    private int _move = 0;
    const int MaxMoves = 9;

    public IEnumerator Cross()
    {
        while (true)
        {
            WriteLine($"Cross, move {_move}");
            if (++_move >= MaxMoves)
            {
                yield break;
            }
            yield return _circle;
        }
    }

    public IEnumerator Circle()
    {
        while (true)
        {
            // code cut off
        }
    }
}
```