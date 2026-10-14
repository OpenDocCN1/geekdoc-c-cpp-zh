```
data Action
  = CreateUser ①
  | Input (State -> State)
  | Check (State -> State)
  | Modal (Modal.Output Message.Output)
  | RouteToLogon
```

① Here’s CreateUser.

Now, look at the code to see what triggers CreateUser and return here once you’ve found the answer.

When I look, I realize that we don’t own the Create Button. It’s owned by Modal. That means that we need to have Modal tell the Inner Component when the buttons have been clicked.

We can do that by creating an H.tell query from Modal to the Inner Component. But, currently when the Parent wants to query the Inner Component, it queries with the Inner Component’s Query Type, what we called iQuery.

But now, we’re going to dictate a Query Type to our Inner Components in Component.Modal as follows:

```
--- COMPILER ERROR!!
data InnerQuery iQuery a ①
  = AffirmativeClicked a ②
  | NegativeClicked a ③
  | PassThroughQuery iQuery a ④
```

① Note the 2 Type Parameters. First, iQuery is the Inner Component’s unique Query Type. And the second is the standard "rest of the computation" Type that all Query Algebras support.

② This will be sent from the Modal to Inner Component when the Affirmative Button has been clicked.

③ This will be sent from the Modal to Inner Component when the Negative Button has been clicked.

④ This is how the Modal’s Parent can send Inner Component specific queries.

Parents of the Modal now will have to send Queries that are unique to the Inner Component using PassThroughQuery.

Add this Type to Component.Modal realizing that there will be compiler errors. Then return here to continue.

The reason for the compiler error is because we have used AffirmativeClick and NegativeClicked again. They were also used in our Action. Let’s rename the Action ones: