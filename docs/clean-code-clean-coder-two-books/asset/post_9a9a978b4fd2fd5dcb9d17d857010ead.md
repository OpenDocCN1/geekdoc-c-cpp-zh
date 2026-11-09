
Paula: “Right. And where do you want it saved?”

Sam: “What do you mean?”

Paula: “Do you want me to save it in a particular sub-directory?”

Sam: “Yes, that’d be good.”

Paula: “What shall we call it?”

Sam: “How about ‘backup’?”

Tom (tester): “Wait, backup is too common a name. What are you really storing in this directory?”

Sam: “The backups.”

Tom: “Backups of what?”

Sam: “The log files.”

Paula: “But there’s only one log file.”

Sam: “No, there are many. One for each day.”

Tom: “You mean that there is one *active* log file, and many log file backups?”

Sam: “Of course.”

Paula: “Oh! I thought you just wanted a temporary backup.”

Sam: “No, the customer wants to keep them all forever.”

Paula: “That’s a new one on me. OK, glad we cleared that up.”

Tom: “So the name of the sub-directory should tell us exactly what’s in it.”

Sam: “It’s got all the old inactive logs.”

Tom: “So let’s call it `old_inactive_logs`.”

Sam: “Great.”

Tom: “So when does this directory get created?”

Sam: “Huh?”

Paula: “We should create the directory when the system starts, but only if the directory doesn’t already exist.”

Tom: “OK, there’s our first test. I’ll need to start up the system and see if the `old_inactive_logs` directory is created. Then I’ll add a file to that directory. Then I’ll shut down, and start again, and make sure both the directory and the file are still there.”

Paula: “That test is going to take you a long time to run. System start-up is already 20 seconds, and growing. Besides, I really don’t want to have to build the whole system every time I run the acceptance tests.”

Tom: “What do you suggest?”

Paula: “We’ll create a `SystemStarter` class. The main program will load this starter with a group of `StartupCommand` objects, which will follow the COMMAND pattern. Then during system start-up the `SystemStarter` will simply tell all the `StartupCommand` objects to run. One of those `StartupCommand` derivatives will create the `old_inactive_logs` directory, but only if it doesn’t already exist.”

Tom: “Oh, OK, then all I need to test is that `StartupCommand` derivative. I can write a simple FitNesse test for that.”

Tom goes to the board.

“The first part will look something like this:”

```text
given the command LogFileDirectoryStartupCommand
given that the old_inactive_logs directory does not exist

when the command is executed
then the old_inactive_logs directory should exist
and it should be empty
```

“The second part will look like this:”

```text
given the command LogFileDirectoryStartupCommand
given that the old_inactive_logs directory exists
and that it contains a file named x
when the command is executed
then the old_inactive_logs directory should still exist
and it should still contain a file named x
```

Paula: “Yeah, that should cover it.”

![](img/d3848357ae109884a140c7b3662e0e30_731_0.png)

To call this a disaster would be a gross understatement. The cost of running the manual test plan is so enormous that they have decided to sacrifice it and simply live with the fact that *they won’t know if half of their product works!*

Professional developers do not let this kind of situation happen. The cost of automating acceptance tests is so small in comparison to the cost of executing manual test plans that it makes no economic sense to write scripts for humans to execute. Professional developers take responsibility for their part in ensuring that acceptance tests are automated.

There are many open-source and commercial tools that facilitate the automation of acceptance tests. FitNesse, Cucumber, cuke4duke, Robot Framework, and Selenium, just to mention a few. All these tools allow you to specify automated tests in a format that nonprogrammers can read, understand, and even author.

## Extra Work

Sam’s point about work is understandable. It *does* look like a lot of extra work to write acceptance tests like this. But given [Figure 7-1](#) we can see that it’s not really extra work at all. Writing these tests is simply the work of specifying the system. Specifying at this level of detail is the only way we, as programmers, can know what “done” means. Specifying at this level of detail is the only way that the stakeholders can ensure that the system they are paying for really does what they need. And specifying at this level of detail is the only way to successfully automate the tests. So don’t look at these tests as extra work. Look at them as massive time and money savers. These tests will prevent you from implementing the wrong system and will allow you to *know* when you are done.

## Who Writes Acceptance Tests, and When?

In an ideal world, the stakeholders and QA would collaborate to write these tests, and developers would review them for consistency. In the real world, stakeholders seldom have the time or inclination to dive into the required level of detail. So they often delegate the responsibility to business analysts, QA, or even developers. If it turns out that developers must write these tests, then take care that the developer who writes the test is not the same as the developer who implements the tested feature.

Typically business analysts write the “happy path” versions of the tests, because those tests describe the features that have business value. QA typically writes the “unhappy path” tests, the boundary conditions, exceptions, and corner cases. This is because QA’s job is to help think about what can go wrong.

Following the principle of “late precision,” acceptance tests should be written as late as possible, typically a few days before the feature is implemented. In Agile projects, the tests are written *after* the features have been selected for the next Iteration or Sprint.

The first few acceptance tests should be ready by the first day of the iteration. More should be completed each day until the midpoint of the iteration when all of them should be ready. If all the acceptance tests aren’t ready by the midpoint of the iteration, then some developers will have to pitch in to finish them off. If this happens frequently, then more BAs and/or QAs should be added to the team.

## The Developer’s Role

Implementation work on a feature begins when the acceptance tests for that feature are ready. The developers execute the acceptance tests for the new feature and see how they fail. Then they work to connect the acceptance test to the system, and then start making the test pass by implementing the desired feature.

Paula: “Peter, would you give me a hand with this story?”

Peter: “Sure, Paula, what’s up?”

Paula: “Here’s the acceptance test. As you can see, it’s failing.”

```text
given the command LogFileDirectoryStartupCommand
given that the old_inactive_logs directory does not exist
when the command is executed
then the old_inactive_logs directory should exist
and it should be empty
```

Peter: “Yeah, all red. None of the scenarios are written. Let me write the first one.”

| scenario | given the command__ | cmd |
| --- | --- | --- |
| create command | @cmd | |

Paula: “Do we already have a createCommand operation?”

Peter: “Yeah, it’s in the CommandUtilitiesFixture that I wrote last week.”

Paula: “OK, so let’s run the test now.”

Peter: (runs test.) “Yeah, the first line is green, let’s move on to the next.”

Don’t worry too much about Scenarios and Fixtures. Those are just some of the plumbing you have to write to connect the tests to the system being tested.

Suffice it to say that the tools all provide some way to use pattern matching to recognize and parse the statements of the test, and then to call functions that feed the data in the test into the system being tested. The amount of effort is small, and the Scenarios and Fixtures are reusable across many different tests.

The point of all this is that it is the developer’s job to connect the acceptance tests to the system, and then to make those tests pass.

## Test Negotiation and Passive Aggression
