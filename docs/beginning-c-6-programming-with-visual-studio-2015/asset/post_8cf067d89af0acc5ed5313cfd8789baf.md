
5. The Owner property requires a callback that should be called whenever the property changes. You can specify this as the second parameter of the constructor of the PropertyMetadata class that is used as the fourth parameter of the register() method. Change the registration like this:

```
public static readonly DependencyProperty OwnerProperty =
    DependencyProperty.Register(
        "Owner",
        typeof(Player),
        typeof(CardsInHandControl),
        new PropertyMetadata(null, new PropertyChangedCallback(OnOwnerChanged)));
```

6. Like the Owner property, the PlayerState and PlayerOrientation properties should also register a callback. Repeat Step 4 for these two properties using the names OnPlayerStateChanged and OnPlayerOrientationChanged for the callback methods.

7. Add the callback methods:

```
private static void OnOwnerChanged(DependencyObject source,
    DependencyPropertyChangedEventArgs e)
{
    var control = source as CardsInHandControl;
    control.RedrawCards();
}
private static void OnPlayerStateChanged(DependencyObject source,
    DependencyPropertyChangedEventArgs e)
{
    var control = source as CardsInHandControl;
    var computerPlayer = control.Owner as ComputerPlayer;
    if (computerPlayer != null)
    {
        if (computerPlayer.State == PlayerState.MustDiscard)
        {
            Thread delayedWorker = new Thread(control.DelayDiscard);
            delayedWorker.Start(new Payload { Deck = control.Game.GameDeck,
                AvailableCard = control.Game.CurrentAvailableCard, Player = computerPlayer });
        }
        else if (computerPlayer.State == PlayerState.Active)
        {
            Thread delayedWorker = new Thread(control.DelayDraw);
            delayedWorker.Start(new Payload { Deck = control.Game.GameDeck,
                AvailableCard = control.Game.CurrentAvailableCard, Player = computerPlayer });
        }
    }
    control.RedrawCards();
}
private static void OnPlayerOrientationChanged(DependencyObject source,
    DependencyPropertyChangedEventArgs e)
{
    var control = source as CardsInHandControl;
    control.RedrawCards();
}
```

8. The callbacks require a number of helper methods. Start by adding the private class and two methods that are used by the delayedWorker threads in the OnPlayerStateChanged method:

```
private class Payload
{
    public Deck Deck { get; set; }
    public Card AvailableCard { get; set; }
    public ComputerPlayer Player { get; set; }
}
private void DelayDraw(object payload)
{
    Thread.Sleep(1250);
    var data = payload as Payload;
    Dispatcher.Invoke(DispatcherPriority.Normal,
new Action<Deck, Card>(data.Player.PerformDraw), data.Deck, data.AvailableCard);
}
private void DelayDiscard(object payload)
{
    Thread.Sleep(1250);
    var data = payload as Payload;
    Dispatcher.Invoke(DispatcherPriority.Normal,
new Action<Deck>(data.Player.PerformDiscard), data.Deck);
}
```

9. Add the methods used to draw the control:

```
private void RedrawCards()
{
    CardSurface.Children.Clear();
    if (Owner == null)
    {
        PlayerNameLabel.Content = string.Empty;
        return;
    }
    DrawPlayerName();
    DrawCards();
}
private void DrawCards()
{
    bool isFaceup = (Owner.State != PlayerState.Inactive);
    if (Owner is ComputerPlayer)
        isFaceup = (Owner.State == PlayerState.Loser ||
Owner.State == PlayerState.Winner);
    var cards = Owner.GetCards();
    if (cards == null || cards.Count == 0)
        return;
    for (var i = 0; i < cards.Count; i++)
    {
        var cardControl = new CardControl(cards[i]);
        if (PlayerOrientation == Orientation.Horizontal)
            cardControl.Margin = new Thickness(i * 35, 35, 0, 0);
        else
```

## 17. Add the DrawDecks method:

```
private void DrawDecks()
{
    controlCanvas.Children.Clear();
    if (CurrentPlayer == null || Deck == null || !GameStarted)
        return;
    List<CardControl> stackedCards = new List<CardControl>();
    for (int i = 0; i < Deck.CardsInDeck; i++)
    {
        stackedCards.Add(new CardControl(Deck.GetCard(i)) { Margin = new Thickness(150 + (i * 1.25), 25 - (i * 1.25), 0, 0), IsFaceUp = false });
        if (stackedCards.Count > 0)
            stackedCards.Last().MouseDoubleClick += Deck_MouseDoubleClick;
        if (AvailableCard != null)
        {
            var availableCard = new CardControl(AvailableCard) { Margin = new Thickness(0, 25, 0, 0) };
            availableCard.MouseDoubleClick += AvailableCard_MouseDoubleClick;
            controlCanvas.Children.Add(availableCard);
        }
    }
    stackedCards.ForEach(x => controlCanvas.Children.Add(x));
}
```

## 18. Finally, add the event handlers for the cards:

```
void AvailableCard_MouseDoubleClick(object sender, MouseButtonEventArgs e)
{
    if (CurrentPlayer.State != PlayerState.Active)
        return;
    var control = sender as CardControl;
    CurrentPlayer.AddCard(control.Card);
    AvailableCard = null;
    DrawDecks();
}
void Deck_MouseDoubleClick(object sender, MouseButtonEventArgs e)
{
    if (CurrentPlayer.State != PlayerState.Active)
        return;
    CurrentPlayer.DrawCard(Deck);
    DrawDecks();
}
```

19. Return to the GameClient.xaml file and remove the Grid that is currently in Row 2. Instead, insert a new dock panel like this:

```
<DockPanel Grid.Row="2">
    <local:CardsInHandControl x:Name="Player2Hand" DockPanel.Dock="Right" Height="380" Game="{Binding}"
        VerticalAlignment="Center" Width="180" PlayerOrientations="Vertical"
        Owner="{Binding Players[1]}" PlayerState="{Binding Players[1].State}" />
    <local:CardsInHandControl x:Name="Player4Hand" DockPanel.Dock="Left" Height="380" VerticalAlignment="Center"
        PlayerOrientation="Vertical" Owner="{Binding Players[3]}" Width="180"
        PlayerState="{Binding Players[3].State}" Game="{Binding}"/>
</DockPanel>
```

```
<local:CardsInHandControl x:Name="Player1Hand" DockPanel.Dock="Top" HorizontalAlignment="Center" Height="154" VerticalAlignment="Top" PlayerOrientation="Horizontal" Owner="{Binding Players[0]}" Width="380" PlayerState="{Binding Players[0].State}" Game="{Binding}"/>
<local:CardsInHandControl x:Name="Player2Hand" DockPanel.Dock="Bottom" HorizontalAlignment="Center" Height="154" VerticalAlignment="Top" PlayerOrientation="Horizontal" Owner="{Binding Players[2]}" Width="380" PlayerState="{Binding Players[2].State}" Game="{Binding}"/>
<local:GameDecksControl Height="180" x:Name="GameDecks" Deck="{Binding GameDeck}">
  AvailableCards="{Binding CurrentAvailableCard}"
  CurrentPlayer="{Binding CurrentPlayer}"
  GameStarted="{Binding GameStarted}"/>
</DockPanel>
```

20. Run the application. By default the ComputerPlayer class is enabled and the number of players is set to two. This means you select a single name in the Start Game dialog box. After that, you should be able to see something like Figure 15-4.

![](img/cf72ea860016d2d680fc085fc06f265a_536_0.png)

FIGURE 15-4

Double-click on the deck or available card to draw and then click a card from your hand to discard it.

## How It Works

Even though there is quite a bit of code in this example, most of it is the dependency properties, and the XAML is all about data binding these properties. The CardsInHandControl creates three properties that it uses to display itself and react to changes: Game, Owner, and PlayerState. Game and Owner are mostly used to draw, but the PlayerState is also used to control the ComputerPlayer actions.

```
private static void OnPlayerStateChanged(DependencyObject source,
    DependencyPropertyChangedEventArgs e)
{
    var control = source as CardsInHandControl;
    var computerPlayer = control.Owner as ComputerPlayer;
    if (computerPlayer != null)
    {
        if (computerPlayer.State == PlayerState.MustDiscard)
        {
            Thread delayedWorker = new Thread(control.DelayDiscard);
            delayedWorker.Start(new Payload
            {
                Deck = control.Game.GameDeck,
                AvailableCard = control.Game.CurrentAvailableCard,
                Player = computerPlayer
            });
        }
        else if (computerPlayer.State == PlayerState.Active)
        {
            Thread delayedWorker = new Thread(control.DelayDraw);
            delayedWorker.Start(new Payload
            {
                Deck = control.Game.GameDeck,
                AvailableCard = control.Game.CurrentAvailableCard,
                Player = computerPlayer
            });
        }
    }
    control.RedrawCards();
}
```

The OnPlayerStateChanged method, which is used to react to changes in the state of the player, determines if the current player is a ComputerPlayer. If it is, it checks to make sure that the computer player draws or discards a card. If this is the case, it creates a worker thread for this to happen and executes the methods on this thread. This allows the application to continue working while the computer is waiting:

```
private void DelayDraw(object payload)
{
    Thread.Sleep(1250);
    var data = payload as Payload;
    Dispatcher.Invoke(DispatcherPriority.Normal,
        new Action<Deck, Card>(data.Player.PerformDraw), data.Deck, data.AvailableCard);
}
```
