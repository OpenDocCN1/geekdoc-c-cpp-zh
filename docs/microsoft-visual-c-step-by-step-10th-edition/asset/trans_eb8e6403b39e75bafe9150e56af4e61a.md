

```csharp
public PlayingCard DealCardFromPack()
{
    var suit = (Suit)randomCardSelector.Next(NumSuits);
    while (this.IsSuitEmpty(suit))
    {
        suit = (Suit)randomCardSelector.Next(NumSuits);
    }
}
```

```csharp
public PlayingCard DealCardFromPack()
{
    ...
    var value = (Value)randomCardSelector.Next(CardsPerSuit);
    while (this.IsCardAlreadyDealt(suit, value))
    {
        value = (Value)randomCardSelector.Next(CardsPerSuit);
    }
}
```

```csharp
public PlayingCard DealCardFromPack()
{
    ...
    var card = this.cardPack[(int)suit, (int)value];
    this.cardPack[(int)suit, (int)value] = null;
    return card;
}
```

```csharp
private bool IsSuitEmpty(Suit suit)
{
    bool result = true;
    for (var value = Value.Two; value <= Value.Ace; value++)
    {
        if (!IsCardAlreadyDealt(suit, value))
        {
            result = false;
            break;
        }
    }
    return result;
}
```

```csharp
private bool IsCardAlreadyDealt(Suit suit, Value value)
    => (this.cardPack[(int)suit, (int)value] == null);
```

```csharp
class Hand
{
    public const int HandSize = 13;
    private PlayingCard[] cards = new PlayingCard[HandSize];
    private int playingCardCount = 0;
    ...
}
```

```csharp
public override string ToString()
{
    string result = "";
    foreach (PlayingCard card in this.cards)
    {
        result += $"{card.ToString()}{Environment.NewLine}";
    }
    return result;
}
```

```csharp
public void AddCardToHand(PlayingCard cardDealt)
{
    if (this.playingCardCount >= HandSize)
    {
        throw new ArgumentException("Too many cards");
    }
    this.cards[this.playingCardCount] = cardDealt;
    this.playingCardCount++;
}
```

```csharp
private void dealClick(object sender, RoutedEventArgs e)
{
    try
    {
        pack = new Pack();
    }
    catch (Exception ex)
    {
        ...
    }
}
```

```csharp
try {
  pack = new Pack();
  for (var handNum = 0; handNum < NumHands; handNum++) {
    hands[handNum] = new Hand();
  }
} catch (Exception ex) {
  ...
}
```

```csharp
try
{
  ...
  for (var handNum = 0; handNum < NumHands; handNum++)
  {
    hands[handNum] = new Hand();
    for (var numCards = 0; numCards < Hand.HandSize; numCards++)
    {
      var cardDealt = pack.DealCardFromPack();
      hands[handNum].AddCardToHand(cardDealt);
    }
  }
}
catch (Exception ex)
{
  ...
}
```

```csharp
try {
  ...
  for (int handNum = 0; handNum < NumHands; handNum++) {
    ...
    north.Text = hands[0].ToString();
    south.Text = hands[1].ToString();
    east.Text = hands[2].ToString();
    west.Text = hands[3].ToString();
  }
  Text = ...
} catch (Exception ex) {
  ...
}
```

```csharp
class Person
{
    public string Name;
    public int Age;

    public Person(string name, int age)
    {
        this.Name = name;
        this.Age = age;
    }
}...
```

```csharp
var names = new[] { new { Name = "John", Age = 57 },
new { Name = "Diana", Age = 57 },
new { Name = "James", Age = 30 },
new { Name = "Francesca", Age = 26 } };
```

```csharp
Person findYoungest()
{
    int youngest = 0;
    for (int i = 1; i < family.Length; i++)
    {
        if (family[i].Age < family[youngest].Age)
        {
            youngest = i;
        }
    }
    return family[youngest];
}
```

```csharp
var mostYouthful = findYoungest();
Console.WriteLine($"Name: {mostYouthful.Name}, Age: {mostYouthful.Age}");
```

```csharp
foreach (Person familyMember in family)
{
    Console.WriteLine($"Name: {familyMember.Name}, Age: {familyMember.Age}");
}
```

```csharp
struct Person
{
    public string Name;
    public int Age;

    public Person(string name, int age)
    {
        this.Name = name;
        this.Age = age;
    }
}
```

```csharp
ref Person findYoungest()
{
    int youngest = 0;
    for (int i = 1; i < family.Length; i++)
    {
        if (family[i].Age < family[youngest].Age)
        {
            youngest = i;
        }
    }
    return ref family[youngest];
}
```

```csharp
ref var mostYouthful = findYoungest();

foreach (Person familyMember in family)
{
    Console.WriteLine($"Name: {familyMember.Name}, Age: {familyMember.Age}");
}
Name: John, Age: 57
Name: Diana, Age: 57
Name: James, Age: 30
Name: Francesca, Age: 26
```

```csharp
// 不要尝试这样做；这无法通过编译
ref int danglingReference()
{
    int i;
    ... // 使用 i 计算一个值
    return ref i;
}
```

```csharp
bool[] flags = { true, false, true, false };
```

```csharp
bool[] flags = ...;
int noOfElements = flags.Length;
```

```csharp
bool initialElement = flags[0];
```

