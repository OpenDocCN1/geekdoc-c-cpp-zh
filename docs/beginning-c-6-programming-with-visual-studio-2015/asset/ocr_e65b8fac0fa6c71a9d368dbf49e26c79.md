```
cards.Add((string)item.imageLink);
}
}
```

8. Lastly, add the markup and Razor code to trigger the consumption of the ASP.NET Web API directly under the code added in step 7:

```
<html>
<head>
<title>BensCards: Deal yourself a hand.</title>
</head>
<body>
@if (IsPost)
{
<label id="labelGoal">Here is your hand of cards.</label>
<br />
<div>
<p><label id="labelPlayer1">Player1: @playerName</label></p>
@foreach (string card in cards)
{
<img width="75"
height="100"
alt="cardImage"
src="https://deckofcards.blob.core.windows.net/carddeck/@card" />
}
</div>
<label id="errorMessageLabel" />
}
else
{
<label id="labelGoal">
Enter the players name and deal the cards.
</label>
<br /><br />
<form method="post">
<div>
<p>Player 1: @Html.TextBox("PlayerName")</p>
<p><input type="submit" value="Deal Hand" class="submit"></p>
</div>
</form>
}
</body>
</html>
```

9. Run the ASP.NET Web Site by pressing F5. Once rendered, enter a name and press the Deal Hand button. The ASP.NET Web Site consumes the ASP.NET Web API and renders a hand of cards, similar to that shown in Figure 17-8.