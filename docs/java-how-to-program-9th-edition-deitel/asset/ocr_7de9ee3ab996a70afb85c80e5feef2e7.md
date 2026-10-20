of class CashDispenser, one object of class Keypad and one object of class DepositSlot. The ATM has a screen, a keypad, a cash dispenser and a deposit slot. (As we saw in Chapter 9, the is-a relationship defines inheritance. We’ll see in Section 13.3 that there’s a nice opportunity to use inheritance in the ATM system design.)

![](bbox=[0.15, 0.24, 0.82, 0.44])

Fig. 12.9 | Class diagram showing composition relationships.

According to the UML specification (www.omg.org/technology/documents/formal/uml1.htm), composition relationships have the following properties:

+   1. Only one class in the relationship can represent the whole (i.e., the diamond can be placed on only one end of the association line). For example, either the screen is part of the ATM or the ATM is part of the screen, but the screen and the ATM cannot both represent the whole in the relationship.

+   2. The parts in the composition relationship exist only as long as the whole does, and the whole is responsible for the creation and destruction of its parts. For example, the act of constructing an ATM includes manufacturing its parts. Also, if the ATM is destroyed, its screen, keypad, cash dispenser and deposit slot are also destroyed.

+   3. A part may belong to only one whole at a time, although it may be removed and attached to another whole, which then assumes responsibility for the part.

The solid diamonds in our class diagrams indicate composition relationships that fulfill these properties. If a has-a relationship does not satisfy one or more of these criteria, the UML specifies that hollow diamonds be attached to the ends of association lines to indicate aggregation—a weaker form of composition. For example, a personal computer and a computer monitor participate in an aggregation relationship—the computer has a monitor, but the two parts can exist independently, and the same monitor can be attached to multiple computers at once, thus violating composition’s second and third properties.

Figure 12.10 shows a class diagram for the ATM system. This diagram models most of the classes that we’ve identified, as well as the associations between them that we can infer from the requirements document. Classes BalanceInquiry and Deposit participate in associations similar to those of class Withdrawal, so we’ve chosen to omit them from this diagram to keep it simple. In Section 13.3, we expand our class diagram to include all the classes in the ATM system.