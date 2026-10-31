+   - **Reusability chance in other tests**

The tests you write during development will also come in handy for the integration tests. In my experience, many production time problems are caused because of differences in the production environment compared to what is expected. If you have an extensive set of tests, you can use them for checking the deployment of the finished application as well. You pay once, but reap the benefits many times over.

To summarize it all, test-friendly design (or testability) is a very important design goal nowadays. It's perhaps the main factor when you make design choices.

# Problems

I have sounded like a salesman for a while. However, there are problems too. Let's have a look at the following:

+   - **UI**

It is hard to use TDD for the UI. TDD fits easier and better with the Domain Model and the core logic, although this isn't necessarily a bad thing. It helps you be strict in splitting the UI from the Domain Model, which is a basic design best practice (so it should be done anyway, but TDD stimulates it). Ensure you write very thin UI and factor out logic from the forms.

+   - **Persistent data**

Databases do cause a tricky problem with TDD because once you have written to the database in one test, the database is in another state when it's time for the next test, and this causes trouble with isolation. You could write your code to set up the database to a well-known state between each test, but that adds to the tester's burden and the tests will run much more slowly.

You could also write tests so that they aren't affected by the changed state, which might reduce the power of the tests a bit. Yet another solution is to use stubs or mock objects to simulate the database apart from during the integration tests when a backup of the database is restored before the tests.

Yet another way is to use transactions purely for the sake of testing. Of course, if your tests focus on the transactional semantics, this isn't a useful solution.

# Note

We will discuss database bound testing more in Chapter 6, "Preparing for Infrastructure."