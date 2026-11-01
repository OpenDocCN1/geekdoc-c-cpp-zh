
For this data binding to work, you must define three dependency properties using techniques you learned in the previous section. These are defined in the code-behind for the user control as follows (they have simple .NET property wrappers, which there is no need to show here because of the simplicity of the code):

```
public static DependencyProperty SuitProperty = DependencyProperty.Register(
    "Suit",
    typeof(CardLib.Suit),
    typeof(CardControl),
    new PropertyMetadata(CardLib.Suit.Club,
new PropertyChangedCallback(OnSuitChanged)));
public static DependencyProperty RankProperty = DependencyProperty.Register(
    "Rank",
    typeof(CardLib.Rank),
    typeof(CardControl),
    new PropertyMetadata(CardLib.Rank.Ace));
public static DependencyProperty IsFaceUpProperty = DependencyProperty.Register(
    "IsFaceUp",typeof(bool),
    typeof(CardControl),
    new PropertyMetadata(true, new PropertyChangedCallback(OnIsFaceUpChanged)));
```

The dependency properties use a callback method to validate their values, and the Suit and IsFaceUp properties also have a callback method for when their values change.

When the value of Suit changes, the OnSuitChanged() callback method is called. This method is responsible for setting the text color to red (for hearts and diamonds) or black (for clubs and spades). It does this by calling a utility method on the source of the method call. This is necessary because the callback method is implemented as a static method, but it is passed the instance of the user control that raised the event as a parameter so that it can interact with it. The method called is SetTextColor():

```
public static void OnSuitChanged(DependencyObject source,
    DependencyPropertyChangedEventArgs args)
{
    var control = source as CardControl;
    control.SetTextColor();
}
```

The SetTextColor() method is private but is obviously still accessible from OnSuitChanged(), as they are both members of the same class, despite being instance and static methods, respectively. SetTextColor() simply sets the Foreground property of the various labels of the control to a solid color brush that is either black or red, depending on the Suit value.

When IsFaceUp changes, the control displays or hides the images and labels that are used to display the current value of the control.

This is all you need to look at in the Card control. The code in the GameClient.xaml.cs code-behind file is included to display the cards and is only temporary. It generates one card for each of the 13 possible values and displays each suit in a column.

```csharp
public Card Draw()
{
    if (cards.Count == 0) return null;

    var card = cards[0];
    cards.RemoveAt(0);
    return card;
}

public Card SelectCardOfSpecificSuit(Suit suit)
{
    Card selectedCard = cards.FirstOrDefault(card => card?.suit == suit);
    if (selectedCard == null) return Draw();
    cards.Remove(selectedCard);
    return selectedCard;
}

public object Clone()
{
    Deck newDeck = new Deck(cards.Clone() as Cards);
    return newDeck;
}

private void InsertAllCards()
{
    for (int suitVal = 0; suitVal < 4; suitVal++)
    {
        for (int rankVal = 1; rankVal < 14; rankVal++)
        {
            cards.Add(new Card((Suit)suitVal, (Rank)rankVal));
        }
    }
}

private void InsertAllCards(List<Card> except)
{
    for (int suitVal = 0; suitVal < 4; suitVal++)
    {
        for (int rankVal = 1; rankVal < 14; rankVal++)
        {
            var card = new Card((Suit)suitVal, (Rank)rankVal);
            if (except?.Contains(card))
                continue;
            cards.Add(card);
        }
    }
}
}
```

6. There will be two types of players in the game: a Player, which is controlled by a real person; and a ComputerPlayer, which is controlled by the game. These two classes are omitted from the code listings here, but you can find them in the code download for the chapter as Player.cs and ComputerPlayer.cs. Go ahead and add them to the CardLib project.

```
CreatePlayers();
InitializeGame();
GameStarted = true;
}
private void InitializeGame()
{
    AssignCurrentPlayer(0);
    CurrentAvailableCard = GameDeck.Draw();
}
private void AssignCurrentPlayer(int index)
{
    CurrentPlayer = Players[index];
    if (!Players.Any(x => x.State == PlayerState.Winner))
        Players.ForEach(x => x.State = (x == Players[index] ? PlayerState.Active :
PlayerState.Inactive));
}
private void InitializePlayer(Player player)
{
    player.DrawNewHand(GameDeck);
    player.OnCardDiscarded += player_OnCardDiscarded;
    player.OnPlayerHasWon += player_OnPlayerHasWon;
    Players.Add(player);
}
private void CreateGameDeck()
{
    GameDeck = new Deck();
    GameDeck.Shuffle();
}
private void CreatePlayers()
{
    Players.Clear();
    for (var i = 0; i < _gameOptions.NumberOfPlayers; i++)
    {
        if (i < _gameOptions.SelectedPlayers.Count)
            InitializePlayer(new Player { Index = i, PlayerName =
_gameOptions.SelectedPlayers[i] });
        else
            InitializePlayer(new ComputerPlayer { Index = i, Skill =
_gameOptions.ComputerSkill });
    }
}
```

17. Finally, add the two event handlers for the events generated by the players:

```
void player_OnPlayerHasWon(object sender, PlayerEventArgs e)
{
    Players.ForEach(x => x.State = (x == e.Player ? PlayerState.Winner :
PlayerState.Loser));
}
void player_OnCardDiscarded(object sender, CardEventArgs e)
{
    CurrentAvailableCard = e.Card;
    var nextIndex = CurrentPlayer.Index + 1 >= _gameOptions.NumberOfPlayers ? 0 :
        CurrentPlayer.Index + 1;
    if (GameDeck.CardsInDeck == 0)
```

```
if (e.Command == GameOptions.OptionsCommand)
    e.CanExecute = true;
if (e.Command == GameViewModel.ShowAboutCommand)
    e.CanExecute = true;
    e.Handled = true;
}

private void CommandExecuted(object sender, ExecutedRoutedEventArgs e)
{
    if (e.Command == ApplicationCommands.Close)
        this.Close();
    if (e.Command == GameViewModel.StartGameCommand)
    {
        var model = new GameViewModel();
        StartGame startGameDialog = new StartGame();
        var options = GameOptions.Create();
        startGameDialog.DataContext = options;
        var result = startGameDialog.ShowDialog();
        if (result.HasValue && result.Value == true)
        {
            options.Save();
            model.StartNewGame();
            DataContext = model;
        }
    }
    if (e.Command == GameOptions.OptionsCommand)
    {
        var dialog = new Options();
        var result = dialog.ShowDialog();
        if (result.HasValue && result.Value == true)
            DataContext = new GameViewModel(); // Clear current game
    }
    if (e.Command == GameViewModel.ShowAboutCommand)
    {
        var dialog = new About();
        dialog.ShowDialog();
    }
    e.Handled = true;
}
```

25. Delete everything from the constructor except the InitializeComponent() call.

## How It Works

Once again you have done a lot of work with very little to show for it when you run the application, but the menus have changed. The Options and New Game menu items have been given shortcut keys and can now be accessed using Ctrl-O and Ctrl-N. This is displayed when you drop down the menus. This has happened because you created two new commands for the menu. You did this in GameOptions.cs and GameViewModel.cs, respectively:

```
public static RoutedCommand OptionsCommand = new RoutedCommand("Show Options",
    typeof(GameOptions), new InputGestureCollection() { new List<InputGesture>
    { new KeyGesture(Key.O, ModifierKeys.Control) }})
public static RoutedCommand StartGameCommand =
```
