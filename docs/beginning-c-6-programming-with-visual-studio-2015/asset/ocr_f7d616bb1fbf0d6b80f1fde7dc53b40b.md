```
var control = source as CardControl;
control.SetTextColor();
}
private static void OnIsFaceUpChanged(DependencyObject source,
    DependencyPropertyChangedEventArgs args)
{
    var control = source as CardControl;
    control.RankLabel.Visibility = control.SuitLabel.Visibility =
        control.RankLabelInverted.Visibility =
        control.TopRightImage.Visibility =
        control.BottomLeftImage.Visibility = control.IsFaceUp ?
        Visibility.Visible : Visibility.Hidden;
}
```

6. Add a property to the class:

```
private Ch13CardLib.Card _card;
public Ch13CardLib.Card Card
{
    get { return _card; }
    private set { _card = value; Suit = _card.suit; Rank = _card.rank; }
}
```

7. Add a helper method to set the text colors and overload the constructor to take a Card:

```
public CardControl(Ch13CardLib.Card card)
{
    InitializeComponent();
    Card = card;
}
private void SetTextColor()
{
    var color = (Suit == Ch13CardLib.Suit.Club || Suit == Ch13CardLib.Suit.Spade) ?
        new SolidColorBrush(Color.FromRgb(0, 0, 0)) :
        new SolidColorBrush(Color.FromRgb(255, 0, 0));
    RankLabel.Foreground = SuitLabel.Foreground = RankLabelInverted.Foreground =
        color;
}
```

8. Add a new value converter by adding a new class to the project. Name it RankNameConverter.cs and add this code:

```
using System;
using System.Windows;
using System.Windows.Data;
namespace KarliCards_Gui
{
    [ValueConversion(typeof(Ch13CardLib.Rank), typeof(string))]
    public class RankNameConverter : IValueConverter
    {
        public object Convert(object value, Type targetType,
            object parameter, System.Globalization.CultureInfo culture)
        {
```