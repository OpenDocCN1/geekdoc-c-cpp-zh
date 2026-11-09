Another common format is Given-When-Then:

Click here to view code image

```
~~~
Given a page with the wiki text: !1 header
When that page is rendered.
Then the page will contain: <h1>header</h1>
~~~
```

It should be clear that these formalisms, whether they are written in an acceptance testing tool or in a simple spreadsheet or text editor, are relatively easy to automate.

# # The Discipline

In the strictest form of the discipline, the acceptance tests are written by BA and QA. BA focuses on the happy path scenarios, whereas QA focuses on exploring the myriad of ways that the system can fail.

These tests are written at the same time as, or just before, the features they test are developed. In an Agile project, divided up into sprints or iterations, the tests are written during the first few days of the sprint. They should all pass by the end of the sprint.

BA and QA provide the programmers with these tests, and the programmers automate them in a manner that keeps BA and QA engaged.

These tests become the *definition of done*. A feature is not complete until all its acceptance tests pass. And when all the acceptance tests pass, the feature is done.

This, of course, puts a huge responsibility on BA and QA. The tests that they write must be full specifications of the features being tested. The suite of acceptance tests *is* the requirements document for the entire system. By writing those tests, BA and QA are certifying that when they pass, the specified features are done and working.

Some BA and QA teams may be unaccustomed to writing such formal and detailed documents. In these cases, the programmers may wish to write the acceptance tests with guidance from BA and QA. The intermediate goal is to create tests that BA and QA *can read* and bless. The ultimate goal is to get BA and QA comfortable enough to write the tests.