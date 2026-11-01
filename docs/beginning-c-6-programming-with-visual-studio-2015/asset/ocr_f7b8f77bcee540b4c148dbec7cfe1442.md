You have now created a simple ASP.NET Web Site using Razor v3. The ASP.NET Web Site connects to the Azure storage account and container for displaying the images of the playing cards.

# How It Works

You certainly noticed a new technology named Razor that was used in the previous exercise. Razor is a view engine that was introduced with ASP.NET 3 MVC along with Visual Studio 2013. Razor, as you have seen, uses C# like language (VB is supported too) that is placed within a @{...} code block and is compiled and executed when the page is requested from a browser. Take a look at this code:

```
@{
Player[] players = new Player[2];
var player1 = Request["PlayerName1"];
var player2 = Request["PlayerName2"];

if (IsPost)
{
    players[0] = new Player(player1);
    players[1] = new Player(player2);
    Game newGame = new Game();
    newGame.SetPlayers(players);
    newGame.DealHands();
}
}
```

The code is encapsulated within a @{...} code block and is compiled and executed by the Razor engine when accessed. When the page is accessed, an array of type Player[] is created and the contents of the query string are populated into the two variables called player1 and player2. If the page is not a post back, which means the page was simply requested (GET) instead of a button click (POST), then the code within the if (IsPost) { } code block does not execute. If the request to the page is a POST, which happens when you click the Deal Cards button, the Players are instantiated, a new game is started, and the hands of cards get dealt.

The initial request to the default.cshtml file executes this code path because it is not a POST.

```
else
{
    <label id="labelGoal">
        Enter the players name and deal the cards.
    </label>
    <br /><br />
    <form method="post">
    <div>
        <p>Player 1: @Html.TextBox("PlayerName1")</p>
        <p>Player 2: @Html.TextBox("PlayerName2")</p>
        <p><input type="submit"
            value="Deal Cards"
            class="submit">
        </p>
    </div>
    </form>
}
```