Furthermore, she assigns

P(Dow = 11,000) = .6.

This problem instance is represented by the decision tree in Figure 8.4. Next we solve the tree:

EU(ICK₁) = (.2)($50,000) + (.8)($200,000) = $170,000

EU(ICK₂) = (.5)($50,000) + (.5)($200,000) = $125,000

EU(Buy ICK) = EU(DOW₁) = (.6)($170,000) + (.4)($125,000) = $152,000

EU(ICK₃) = (.3)($0) + (.7)($250,000) = $175,000

EU(ICK₄) = (.6)($0) + (.4)($250,000) = $100,000

EU(Buy option) = EU(DOW₂) = (.6)($175,000) + (.4)($100,000) = $145,000

EU(D) = max($152,000, $145,000) = $152,000.

The solved decision tree is shown in Figure 8.5. The decision is to buy ICK. ■

The previous example illustrates a problem with decision trees. That is, the representation of a problem instance by a decision tree grows exponentially with the size of the instance. Notice that the instance in Example 8.3 only has one more element in it than the instance in Example 8.2; that is, it includes that uncertainty about the Dow. Yet its representation is twice as large. So it is quite difficult to represent a large instance with a decision tree. We will see in the next section that influence diagrams do not have this problem. Before that, we show more examples.

**Example 8.4** Sam has the opportunity to buy a 1996 Spiffycar automobile for $10,000, and he has a prospect who would be willing to pay $11,000 for the auto if it is in excellent mechanical shape. Sam determines that all mechanical parts except for the transmission are in excellent shape. If the transmission is bad, it will cost Sam $3000 to repair it, and he would have to repair it before the prospect would buy it. So he would only end up with $8000 if he bought the vehicle and its transmission was bad. He cannot determine the state of the transmission himself. However, he has a friend who can run a test on the transmission. The test is not absolutely accurate. Rather, 30% of the time it judges a good transmission to be bad and 10% of the time it judges a bad transmission to be good. To represent this relationship between the transmission and the test, we define the following random variables:

| Variable | Value | When the Variable Takes This Value |
| :--- | :--- | :--- |
| Test | positive | Test judges the transmission to be bad. |
| | negative | Test judges the transmission to be good. |
| Tran | good | Transmission is good. |
| | bad | Transmission is bad. |