# Getting started

Cribbage is a card game where hands are counted up into points, and the first player to score 121 points wins. It’s up to the players to count up the points, and the score is kept on a board.

Cribbage boards are made up of two lines of holes for pegs, usually totaling 120, but sometimes 60 holes are used and you play through twice. Figure 5-1 shows a typical cribbage board. Cribbage boards come in a bunch of styles — check out www.cribbage.org if you’re curious; it has a great gallery of almost 100 boards, from basic to whimsical.

For this example, I create the board image for an application that keeps score of a cribbage game — but it wouldn’t be beyond C# to write the cards into the game, too!

So the board for this application has 40 holes on each of three pairs of lines, which is the standard board setup for two players playing to 120, as shown in Figure 5-2. The first task is to draw the board and then to draw the pegs as the players’ scores — entered in text boxes — change.

![](bbox=[0.24, 0.5, 0.86, 0.89])

Figure 5-1:
A traditional
cribbage
board.