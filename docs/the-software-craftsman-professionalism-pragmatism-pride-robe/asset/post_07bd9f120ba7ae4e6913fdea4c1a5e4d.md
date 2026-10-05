
Some of the features were simple, but others so much. The back-solution, which had to be compliant with a bunch of rules and nonfunctional requirements, was far from trivial to implement. This feature was composed of a few cases which all had to be ordered to be meaningful to the users. The problem was that neither the business knew how things should work at the detail level. Reducing, which meant fewer features, did not make sense in this case—we had a big deadline to meet and could release new versions of the application respectively. Then thin slices, with fully functional features, would take too long to give them feedback; they wanted to see if the whole would make sense—how the features would work better.

We then proposed a quicker solution: to use thin slices, with respect to pages, as views where users could not change the data easily and with all data cached in memory. The data, which we would live with many pages, would be files at startup and stored in data structures in memory. We would build the majority of the pages—just displaying the data and providing the appropriate behavior (AJAX cases, rich behavior, styling, etc.). This would give users a better idea of how the application would work. We then enabled a few pages to actually change data (editing, deleting, and updating), but just in memory. We needed to prove that the application could work without physical persistence, yet with all the adding that was needed for any application inside the bank, and without the performance issues.

With this approach, we were able to build a functional application quickly, deploying new versions at a time for user acceptance testing (UAT). Product owners and business analysts had the opportunity to quickly look at the application and ask for changes. As we built a horizontal slice of the application, our code was extremely simple—there were no data migrations or complex domain logic.

After some time, we had a better idea about how the system should behave. We discovered which pages we needed to use more often, and by bit by bit, we started database persistence and the appropriate business logic. We live with many pages, just a few where users could actually change data. For changing the data that could not be changed by the users (our pages), we prepared new data files with the desired change, bound the application, and deployed them as needed.

The application was test-driven. We didn't abandon our practices because we were using 'specs'. We were experienced TDD practitioners, and testing was not a bottleneck for all of us—TDD didn't slow us down. In fact, we made so much faster to go the large number of changes we had in a short period of time. Although we were speaking, we didn't want bugs to be in there. The versions deployed into UAT were used for demos to clients. While, speaking, we fixed bugs and discarded as needed.

Over the period of a year, we had one small bug in production and a few small bugs in what, which were very quickly. There were times when the complexity of requirements and features slowed down, but never the unit tests slowed us to release and quickly. Tests helped us to make sure that all half-baked ideas from the business work correctly, and met their expectations. Changing the code every time they changed their mind was easy as simple, flexible, and we could make sure that a change in one place in the code would not break other parts of the

The point is not about vertical horizontal slices. The point is not about when we write tests. The point is about figuring out what we need, and the best way of doing it is to be able to change the code almost fast as they change—without breaking anything. In order to achieve that, the project I described, TDD, continuous integration, and pairing programming were essential for us.

The problem is not about unexpected changes in a software project; the problem is inability to cope with them. Well-crafted software is a means to an end, where the goal is to provide value to our clients. In any project of significant size, well-crafted code made us go faster and better precision.

# Software Projects Are Not About Us

As professionals, we need to understand that a software project is not about us and ours. The I-know-what'm-doing-and-I't-need-to-write-tests is selfish and arrogant. Even if that were true, the project is not about you. It is not about one or two great developers. We need to think about how going to maintain the software we value. We need to think about how difficult it is for the company to keep evolving the software. If the value we add to a project is to continuous improvement in the project, it's not yours. A value of a clients.

# Great Versus Mediocre

Passionate developers love writing code. They enjoy creating complex solutions in order to keep themselves interested in jobs. They sometimes create complex solutions just because they are bored—the business-related features are just too dull. They are proud of all the architecture and the design patterns they create and use. In the 990s, complex and cryptic code was a sign of seniority. You were considered senior when you wrote code that no one else could understand. "I have no idea what this code does The guy who wrote it must be really good." The good news is we were wrong about that and how we know it.

Any typical developer can make work. What distinguishes great from mediocre developers is how they make things work. Great developers write simple code that satisfies the business requirements, and less-experienced developers have no problem identifying. Solving the problem with a simple and elegant solution is harder than solving with a complex and overengineered one. I believe that all the horrible code out there is not proof of that. Great developers go beyond simple and short solutions; they strive to solve problems without writing any code at all. The best line of code is the one you don't

Well-crafted code is simple, testable, easy to understand, and most importantly, does the

# Four Rules of Simple Design

Before thinking about architecture, design patterns, or anything else, we follow the "Four Rules of Simple Design," as defined by Kent Beck:

- Pass all tests
- Minimize duplication
- Maximize clarity
- Have fewer elements

Over the years, many people reowed these elements. Combined with the knowledge of Domain-Driven Design and the SOLID principles, this approach is normally enough to achieve well-crafted code.

The Generic code is a good thing but it doesn't come for free. The more generic the code is, the more it becomes useless

# Refactoring to Patterns

It turns out these Ivory-Tower Architects are not entirely wrong. They are wrong to say we should keep doing a design up front (BDUF), but they are right to say we should not throw away decades of knowledge. Professional TDDers rarely use design patterns from the outset. We write our tests according to the business requirements, and we write enough code to satisfy the tests. This usually leads to a very specific, but much simpler,
