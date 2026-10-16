![](bbox=[0.115, 0.103, 0.815, 0.37])

# Figure 10.6

One player wins; the other is not so lucky.

# Table 10.1 Blackjack Classes

| Class | Base Class | Description |
|---|---|---|
| Card | None | A Blackjack playing card. |
| Hand | None | A Blackjack hand. A collection of Card objects. |
| Deck | Hand | A Blackjack deck. Has extra functionality that Hand doesn’t, such as shuffling and dealing. |
| GenericPlayer | Hand | A generic Blackjack player. Not a full player, but the common elements of a human player and the computer player. |
| Player | GenericPlayer | A human Blackjack player. |
| House | GenericPlayer | The computer player, the house. |
| Game | None | A Blackjack game. |

In addition to describing your classes in words, it helps to draw a family tree of sorts to visualize how your classes are related. That’s what I did in Figure 10.7.

Next, it’s a good idea to get more specific. Ask yourself about the classes. What exactly will they represent? What will they be able to do? How will they work with the other classes?