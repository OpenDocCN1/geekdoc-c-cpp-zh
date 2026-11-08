The QA manager is holding this document out to me because he just got back from his boss’ office. His boss just got back from the CEO’s office. The year is 2008. The great recession has begun. The CFO cut that million dollars in half every six months. The QA manager is holding this document out to me asking me which half of these tests he shouldn’t run.

I told him that no matter how he decided to cut the tests, he wouldn’t know if half of his system was working.

This is the inevitable result of manual testing. Manual tests are always eventually lost. What you just heard was the first and most obvious mechanism for losing manual tests: manual tests are *expensive* and so are always a target for reduction.

However, there is a more insidious mechanism for losing manual tests. Developers seldom deliver to QA on time. This means that QA has less time than planned to run the tests they need to run. So, QA must *choose* which tests they believe are most appropriate to run in order to make the shipment deadline. And so some tests aren’t run. They are lost.

And besides, humans are not machines. Asking humans to do what machines can do is expensive, inefficient, and *immoral*. There is a much better activity for which QA should be employed—an activity that uses their human creativity and imagination. But we’ll get to that.

Customers and users expect that every new release is thoroughly tested. No one expects the development team to bypass tests just because they ran out of time or money. So every test that can feasibly be automated must be automated. Manual testing should be limited to those things that cannot be automatically validated and to the creative discipline of Exploratory Testing.^5

The Agile practices of TDD, Continuous Integration, and Acceptance Testing support this expectation.

5. Agile Alliance. Exploratory testing. Accessed at https://www.agilealliance.org/glossary/exploratory-testing.