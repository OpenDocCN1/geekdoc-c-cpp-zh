
*Good collaboration removes some of the blocks people have to do their jobs but does not necessarily make them more skilled.*

There is a big expectation that comes with Agile adoption: development teams should deliver production-ready software as soon as a feature is done, or at the least at the end of each iteration. For most development teams, that is a significant change. There is no way they can achieve that by changing the way they work, and that means learning and mastering new practices. But there are a few problems. Rarely is there a budget for up-skilling developers during Agile transformations. Business does not expect developers to slow down during their Agile adoption. Most do not even know developers have to learn new practices. They were told that if they worked in a more collaborative way, developers would work faster.

Releasing software to production every two weeks requires a lot of discipline and technical skills—skills that are not commonly found in teams used to delivering software a few times per year. Things get much worse when multiple teams, with quite a few developers each, all working on the same systems, are expected to deliver features to production as they finish them. The level of mastery in technical practices and engineering must be extremely high for teams to deploy software to production multiple times a day without compromising the overall stability of the system. Developers cannot just pick an item from the top of a product backlog, start coding, and think that everything is going to be OK when they push to production. They need strategic thinking. They need a modular design that supports parallel work. They need to continuously embrace change while making sure the system can always be deployed to production. For that, they need to continuously build software that is both flexible and robust. But balancing flexibility and robustness with the need to deploy software to production continuously is extremely hard and cannot be done without the necessary engineering skills.

It is not realistic to think that teams will develop these skills simply by creating a more collaborative environment. Teams need support in acquiring these technical skills. This support can happen through a combination of coaching, training, experimentation, and self-learning. Business agility is directly related to how quickly companies can evolve their software, and that means an evolution in their engineering skills and technical practices.

## MOVING APART

Of course, not every Agile transformation or company suffers from all the problems described earlier, or at least not to the same degree. In terms of business, it is fair to say that most companies that have gone through an Agile transformation, even if partially, are in a better place today. They are working in shorter iterations. The collaboration between business and technology is closer than it was before. Problems and risks are being identified earlier. Businesses are reacting faster as they get new information, truly benefiting from an iterative approach to software development. However, although companies are indeed better than they were before, the split between Agile processes and engineering are still hurting them. Most modern Agile coaches do not have enough (if any) technical skills to coach developers on technical practices, and they rarely talk about engineering. Over the years, developers started seeing Agile coaches as another layer of management: people telling them what to do instead of helping them to get better at what they do.

> *Are developers moving away from Agile, or is Agile moving away from developers?*

The answer to this question is probably both. It seems that Agile and developers are moving away from each other. In many organizations, Agile has become synonymous with Scrum. XP, when present, is reduced to a few technical practices like TDD and Continuous Integration. There is an expectation from Agile coaches that developers apply some of the XP practices, but they do not really help or get involved in the way developers are working. Many Product Owners (or project managers) still do not feel they are part of the team and do not feel responsible when things do not go according to plan. Developers still need to negotiate hard with the business to make the necessary technical improvements to keep developing and maintaining the system.

> *Companies are still not mature enough to understand that technical problems are in fact business problems.*

With a diminishing focus on technical skills, can Agile significantly improve software projects beyond what it did up until now? Is Agile still focused on *uncovering better ways of developing software by doing it and helping others do it*, as it was written in the Agile Manifesto? I'm not so sure.

## SOFTWARE CRAFTSMANSHIP

To raise the bar of professional software development and re-establish some of the original Agile goals, a group of developers met in November 2008 in Chicago to create a new movement: Software Craftsmanship. In that meeting, similar to what happened during the Agile summit in 2001, they agreed on a core set of values and came up with a new manifesto¹ that was built on top of the Agile Manifesto:

> As aspiring Software Craftsmen, we are raising the bar of professional software development by practicing it and helping others learn the craft. Through this work we have come to value:
>
> - Not only working software, but also well-crafted software
> - Not only responding to change, but also steadily adding value
> - Not only individuals and interactions, but also a community of professionals
> - Not only customer collaboration, but also productive partnerships
>
> That is, in pursuit of the items on the left we have found the items on the right to be indispensable.

The Software Craftsmanship manifesto describes an ideology, a mindset. It promotes professionalism through different perspectives.

Well-crafted software means code that is well designed and well tested. It is code that we are not scared to change and code that enables business to react fast. It is code that is both flexible and robust.

Steadily adding value means that no matter what we do, we should always be committed to continuously provide increasing value to our clients and employers.

A community of professionals means that we are expected to share and learn with each other, raising the bar of our industry. We are responsible for preparing the next generation of developers.

¹ http://manifesto.softwarecraftsmanship.org

better practices are discovered. But that does not mean that the international Craftsmanship community does not advocate any practices. On the contrary, since its creation in 2008, the Software Craftsmanship community considers XP the best set of Agile development practices currently available. TDD, Refactoring, Simple Design, Continuous Integration, and Pair Programming are heavily advocated by the Software Craftsmanship community—but they are XP practices, not Craftsmanship practices. And they are not the only practices. Craftsmanship also promotes Clean Code and SOLID principles. It promotes small commits, small releases, and Continuous Delivery. It promotes modularity in software design and any type of automation that removes manual and repetitive work. And it promotes any practices that improve productivity, reduce risk, and help to produce valuable, robust, and flexible software.

Craftsmanship is not only about technical practices, engineering, and self-improvement. It is also about professionalism and enabling clients to achieve their business goals. And this is an area where Agile, Lean, and Craftsmanship are in perfect alignment. All three have similar goals but tackle the problem from different but equally important and complementary perspectives.

### FOCUS ON THE VALUE, NOT THE PRACTICE

A common mistake in the Agile and Craftsmanship communities is to promote practices instead of the value they provide. Let’s take TDD as an example. One of the most common questions asked inside the Craftsmanship communities is “How do I convince my manager/colleague/team to do TDD?” That is the wrong question. The problem here is that we are offering a solution before agreeing on the problem. People will not change the way they work if they do not see the value.

Instead of pushing TDD, maybe we could start agreeing on the value of reducing the time it takes to test our entire system. How long does it take today? Two hours? Two days? Two weeks? How many people are involved? What if we could reduce it to 20 minutes? Two minutes? Maybe even
