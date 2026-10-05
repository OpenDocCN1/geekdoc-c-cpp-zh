
solution to the problem. Just keep it enough, not more. We use the refactoring phase from the TDD lifecycle, (red, green, refactor) to make sure all duplications are removed and the domain is appropriately expressed in code.

Let's say we had a system where one of the features was to calculate the salaries of permanent employees. This feature was test-driven and specifically to satisfy the original requirement. After a few months, when a business decides to employ contractors, and we now have to implement a feature that calculates their payments. That is, when before creating the code that they need, we refactor and redesign the code by creating a payment strategy, adjust the design to accommodate the new abstraction and introduce the new contractor payment strategy that can be easily added to the code. We can do this by "just-in-time" design, making the code we prepared (redesigned) to gracefully receive the new features.

There is a price to pay every time we introduce an abstraction or, in words, a level of indirection. Before, the code might require frequent refactoring. Now it is a bit harder—it is not straightforward to understand why payment strategy is better used time. We would need to look for configuration or classes. When we have two payment strategies, we can justify the added complexity of the code.

Introducing abstractions early, with no justification other than "we may need it in the future," is what makes applications complicated. Since we don't know which part of the system will grow or evolve, and we now introduce abstractions (complexity) everywhere. We think when we are being smart, trying to prepare our applications to grow in every single direction. But that is not smart; it is:

There will be a few parts of code where the effort of introducing abstractions will pay off, but for the rest small refactorings become a pain. The pragmatic approach would be to introduce abstractions only when needed to keep the overall complexity level low. A system with low complexity is always easier to maintain and a system with a higher complexity level

Details are always, but part of our toolkit. However, that doesn't mean we should always use them. When we are refactoring the code to introduce new layers or abstractions, we can then go one step further, potentially refactoring the code to an appropriate pattern that is commonly used to solve that type of problem. Instead of choosing your favorite set of patterns, guided by your own bias and trying to make your project domain fit into them, focus on solving the problem at hand. Small refactorings are based on the project requirements and principles. If you find that the solution is the same as one defined by a design pattern, proceed further and refactor your code toward generic. Generic code, although more extensive, is more complex than simple code. Instead of always striving for generic code, write what is the problem you are trying to solve and make it generic when you have a reason to:

I remember the early days of my career. "We have a new application to build? Let's define the architecture for it. What patterns should we use this time? We would then spend days designing the architecture. 'Cool, looks great. Now let's speak to the business people and figure out what we are trying to solve.' Teenagers, huh?

# Craftsmanship and Pragmatism

Craftsmanship is not craftsmanship. A craftsman's primary focus is customer satisfaction. Quality, time and cost are part of this satisfaction. Code cannot be considered well-crafted if it doesn't provide value to away.

It's vital to understand what customers are achieving with a software project. Some projects need to be done quickly, because market opportunity. Other projects have long-term goals. Different projects have different needs. However, no matter how big the project is, a craftsman will always produce quality code. Quick doesn't mean large. Large projects don't mean BDUF or overengineering. Clean and well-crafted code is important—it means having the ability to quickly and make safe changes to the business needs. One of the best ways we have to help the business to achieve their goals is to be able to change the code as quickly as they change their minds.

# Summary

Quality is not essential. The lack of skill is what makes well-crafted software expensive. TDD doesn't slow developers. Testing is not a bottleneck. Learning and mastering a new skill, practice, or technology.

Regardless of what managers and product owners say, they all expect quality. They would always choose quality if they didn't need it for something else, like time and money.

Our job as craftsmen is to lower the cost of quality to a point that it is not a concern anymore. For that, we need to master our practices and be pragmatic. We need to understand the value that certain practices bring in different contexts. When dealing with customers, clients should never pay more for quality.

# 16. Career As a Software Craftsman

Being a software developer is awesome. Look around. Everything that is man-made today has software behind it. The chair you are sitting on comes from a factory that uses software. TVs, refrigerators, and cars all have software running inside them. The food you eat is connected to software—if not for the many companies using millions of lines of code in their systems, from so many suppliers and countries wouldn't have marketplaces. Software lives—many of the advancements in modern life were possible because of software. Transport, communications, entertainment, sports, everything has benefited. Software enables businesses to succeed and thrive, empowers people in need. Software provides vital support for the authorities and volunteers to help, minimizing suffering after natural disasters. Software helps to prevent, injustices, assists law enforcement, and helps restore water, electricity, and communication to remote parts of the world. Software also gives us cold beer and herds of cattle in our TV boxes. Software unites families and friends, and for one another, life becomes less lonely. What? How can we treat our jobs as “just a job?” Can we not care when we know that what we do is important, sometimes essential, for our own lives? Software developers are essential for the future of the world we live in.

In this chapter we will discuss what it is to be a craftsman and how to have a successful and fulfilling career.

# Being a Craftsman

Passion. That summarizes all. Software craftsmen are passionate about software development and profession. They are passionate about solving problems with simple solutions. It is a life of continuous learning, teaching, and sharing. Software craftsmen are passionate about helping the industry to evolve; sharing craft; mentoring developers through their experiences via blogs, talks, videos, and conversations; and being active in technical communities. Software craftsmen are always, ready to learn from more-experienced developers, and help the less experienced.

It is no secret that software is only going to grow in the next few decades, making everyone ever more dependent on it. It is our to do well with this demand, software craftsmen feel they have a social and moral obligation to pay the next generation of craftsmen, making our industry better and more than before.

Being a craftsman is more than being who writes good code and delivers business value. It’s a lifestyle. A life where we choose to do things well, to help others learn. It’s a life of dedication to the art of writing code. Being a craftsman means to explore and experiment with new ideas not to be dogmatic about tools, languages and frameworks.

True software craftsmen focus on solving problems, not on writing code. When they need to leave behind they were the only one who could understand the code it is easy to maintain. A craftsman is needed for the right reasons. No developer will leave a craftsman because the mess they left was the only one who could understand the code. A craftsman is needed for the right reasons: insightful contributions, encouragement, knowledge, and most, being a great colleague.
