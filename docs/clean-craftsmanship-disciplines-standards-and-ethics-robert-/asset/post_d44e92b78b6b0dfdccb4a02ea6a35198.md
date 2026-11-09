
And this passes. The next test in the sequence passes too:

Click here to view code image

```
assertWrapped("x x", 3, "x x");
```

What’s next? We could try these:

Click here to view code image

```
assertWrapped("x x", 1, "x\nx\nx\nx");
assertWrapped("x x", 2, "x\nx\nx\nx");
assertWrapped("x x", 3, "x\nx\nx");
assertWrapped("x x", 4, "x x\nx");
assertWrapped("x x", 5, "x x");
```

They all pass. There’s probably not much point in adding the fourth x. Let’s try this:

Click here to view code image

```
assertWrapped("xx xx", 1, "x\nx\nx\nx");
```

That one passes. And so do the next two tests in the sequence:

Click here to view code image

```
assertWrapped("xx xx", 2, "xx\nxx");
assertWrapped("xx xx", 3, "xx\nxx");
```

But the next test fails:

Click here to view code image

```
assertWrapped("xx xx", 4, "xx\nxx");
```

It fails because it returns "xx x\nx". And that’s because it did not break on the space between the two “words.” Where is that space? It’s *before* the *w*th character. So, we need to search backwards from *w* for a space:

Click here to view code image

```
private String wrap(String s, int w) {
  if (w >= s.length())
    return s;
  else {
```

## Enter BDD

In 2003, while practicing and teaching TDD, Dan North, in collaboration with Chris Stevenson and Chris Matts, made the same discovery that Bill Wake had made. However, they used a different vocabulary: Given-When-Then (GWT).

This was the beginning of *behavior-driven development* (BDD).

At first, BDD was viewed as an improved way of writing tests. Dan and other proponents liked the vocabulary better and affixed that vocabulary into testing tools such as JBehave, and RSpec.

As an example, I can rephrase the `gutterGame` test in BDD terms as follows:

Click here to view code image

```
    Given that the player rolled a game of 20 gutter balls,
    When I request the score of that game,
    Then the score will be zero.
```

It should be clear that some parsing would have to take place in order to translate that statement into an executable test. JBehave and RSpec provided affordances for that kind of parsing. It also ought to be clear that the TDD test and the BDD test are synonymous.

Over time, the vocabulary of BDD drew it away from testing and toward the problem of system specification. BDD proponents realized that even if the GWT statements were never executed as tests, they remained valuable as specifications of behavior.

In 2013, Liz Keogh said of BDD:

> *It’s using examples to talk through how an application behaves. ... And having conversations about those examples.*

Still, it is hard to separate BDD entirely from testing if only because the vocabulary of GWT and AAA are so obviously synonymous. If you have any doubts about that, consider the following:

- *Given* that the test data has been *Arranged*
- *When* I execute the tested *Act*
- *Then* the expected result is *Asserted*

## Finite State Machines

The reason I made such a big deal out of the synonymity of GWT and AAA is that there is another famous trait that we frequently encounter in software: the transition of a finite state machine.

Consider the state/transition diagram of a simple subway turnstile (Figure 3.1).

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_133_0.png)

**Figure 3.1** Transition/state diagram for a subway turnstile

The turnstile starts in the locked state. A coin will send it to the unlocked state. When someone passes through, the turnstile returns to the locked state. If someone passes without paying, the turnstile alarms. If someone drops two coins, the extra coin is refunded.

This diagram can be turned into a state transition table as follows:

| Current State | Event | Next State |
|---|---|---|
| Locked | Coin | Unlocked |
| Locked | Pass | Alarming |
| Unlocked | Coin | Refunding |
| Unlocked | Pass | Locked |
| Refunding | Refunded | Unlocked |
| Alarming | Reset | Locked |

Each row in the table is a transition from the current state to the next state triggered by the event. Each row is a triplet, just like GWT or AAA. More important, each one of those transition triplets is synonymous with a corresponding GWT or AAA triplet, as follows:

Click here to view code image

```
Given it is in the Locked state
When it gets a Coin event
Then it transitions to the Unlocked state.
```

What we can deduce from this is that *every test you write is a transition of the finite state machine that describes the behavior of the system.*

Repeat that to yourself several times. Every test is a transition of the finite state machine you are trying to create in your program.

Did you know that the program you are writing is a finite state machine? Of course it is. Every program is a finite state machine. That’s because computers are nothing more than finite state machine processors. The computer itself transitions from one finite state to the next with every instruction it executes.

Thus, the tests you write when practicing TDD and the behaviors you describe while practicing BDD are simply transitions of the finite state machine that you are attempting to create. Your test suite, if it is complete, *is that finite state machine.*

The obvious question, therefore, is how do you ensure that all the transitions you desire your state machine to handle are encoded as tests? How do you ensure that the state machine that your tests are describing is the complete state machine that your program should be implementing?

using *mock objects*, they likely thought nothing of it. Indeed, when I presented the idea of a mock object in Java to one expert Smalltalker and TDDer in 1999, his response to me was: “Too much mechanism.”

Nevertheless, the technique caught hold and has become a mainstay of TDD practitioners.

But before we delve too much further into the technique itself, we need to clear up a vocabulary issue. Almost all of us use the term *mock object* incorrectly—at least in a formal sense. The mock objects we talk about nowadays are very different from the mock objects that were presented in the endo-testing paper back in 2000. So different, in fact, that a different vocabulary has been adopted to clarify the separate meanings.

In 2007, Gerard Meszaros published *xUnit Test Patterns: Refactoring Test Code*.^2 In it, he adopted the formal vocabulary that we use today. Informally, we still talk about mocks and mocking, but when we want to be precise, we use Meszaros’s formal vocabulary.

2. Gerard Meszaros, *xUnit Test Patterns: Refactoring Test Code* (Addison-Wesley, 2007).

Meszaros identified five kinds of objects that fall under the informal mock category: dummies, stubs, spies, mocks, and fakes. He called them all *test doubles*.

That’s actually a very good name. In the movies, a stunt double stands in for an actor, and a hand double stands in for closeups of an actor’s hands. A body double stands in for shots when the body, and not the face, of the actor is on screen. And that’s just what a test double does. A *test double* stands in for another object while a test is being run.

Test doubles form a type hierarchy of sorts (Figure 3.2). Dummies are the simplest. Stubs are dummies, spies are stubs, and mocks are spies. Fakes stand alone.

![](img/7b01f9dd5d5d33f16ee27a44427cd56e_137_0.png)

**Figure 3.2** Test doubles

The mechanism that all test doubles use (and which my Smalltalker friend thought was “too much”) is simply polymorphism. For example, if you want to test the code that manages an external service, then you isolate that external service behind a polymorphic interface, and then you create an implementation of that interface that stands in for the service. That implementation is the test double.

But perhaps the best way to explain all this is to demonstrate it.

## Dummy

Test doubles generally start with an interface—an abstract class with no implemented methods. For example, we could start with the `Authenticator` interface:

[Click here to view code image](#)

```java
public interface Authenticator {
  public Boolean authenticate(String username, String password);
}
```

The intent of this interface is to provide our application with a way to authenticate users by using usernames and passwords. The `authenticate` function returns `true` if the user is authentic and `false` if not.

Now let’s suppose that we want to test that a `LoginDialog` can be cancelled by clicking the close icon before the user enters a username and password. That test might look like this:

[Click here to view code image](#)

```java
@Test
public void whenClosed_loginIsCancelled() throws Exception {
  Authenticator authenticator = new ???;
  LoginDialog dialog = new LoginDialog(authenticator);
  dialog.show();
  boolean success = dialog.sendEvent(Event.CLOSE);
  assertTrue(success);
}
```

Notice that the `LoginDialog` class must be constructed with an `Authenticator`. But that `Authenticator` will never be called by this test, so what should we pass to the `LoginDialog`?

Let’s further assume that the `RealAuthenticator` is an expensive object to create because it requires a `DatabaseConnection` passed in to its constructor.
