
where one developer writes the test and the other writes the code to make it pass; switching roles every time a test passes); after the keyboard and if she wants to write the next test. Make sure you have fun together.

Introducing TDD to someone who is easier to learn is quite easy. If you are not very good at it, you can learn together. On the other hand, it can be very tricky to introduce TDD to someone who is skeptical about it. In this case, I suggest that you make sure you are comfortable with TDD before trying it. The last thing you want is to have a skeptic developer, pairing with you thinking that TDD is too hard, takes too long, and hence not worth it.

Developers are creatures of habit and are generally very opposed. You cannot just go there and tell them what to do. The most effective way to introduce a practical technique is by example. Ask them to pair with you and show them how you do it.

## Facing the Skeptic

We started talking about the categories that skeptics may fall into. Now, we have already discussed the most important things we need to know and how to deal with all of them. There are just a few others we should know.

Practicing in our spare time, preparing ourselves, and being able to demonstrate our technique can take a long way when drives. We can easily inform the Uniform, the shepherd the Herd, the Cynic, understand where the Bent person went wrong and their reason, and reduce the team's learning curve, which addresses the Cynic's concerns.

Being able to communicate and at the right level is also important. If you want to bring the boss to your side, speak their language. Don't bring developers' problems. Raise the conversation to them. Improving productivity, reducing cost, increasing revenue, meeting deadlines, reducing the number of bugs, keeping a steady predictable velocity, and satisfying requirements that the Boss will care about. If you want to change something, how this change would affect some of the things they care about.

Irrational issues. Besides the technical issues, there are some issues being discussed with Irrationals. Focus on people who are willing to have a rational debate and know what people want to say about you. Irrationals are irritating people and there is a high chance that the team will ignore them again, regardless of whether they agree with what you are proposing.

Make sure you explain the decision-making process. Include your opinion. Propose that the team uses isolation boundaries to try new things. Making new things are not seen as a threat to anyone's job. Your objective is to make things better, not to become the Boss or claim the credit for it. You need to establish that you are a better developer than any other developer. With this establishment, no developer will fall into the Insecurity category.

## The Ivy-Tower Architect

The Ivy-Tower Architect will probably be the most skeptic to deal with. A true clash of values and ideas of how things should be done. While a software craftsman would consider following an Agile approach to software development, the Architect will try to push for a big upfront design, trying to define the technology and architecture before understanding the problems we are trying to solve. The Architect imposes their vision on the development but does not work with the team on a daily basis to understand and how their decisions are affecting the process.

The Ivy-Tower Architect is in a position of authority, having the responsibility to look after a department or even a whole company. They may draw individuals as boxes in Powerpoint presentations but she won't understand all the details of each of them. The Ivy-Tower Architects are not part of any development team and don't write code, they never feel the pain caused by their ill-defined architecture decisions.

## Responsibility Accountability

Ivy-Tower Architects are responsible for all the decisions and think developers are just a bunch of coders implementing their vision. Technical debates with Ivy-Tower Architects can be soul-draining.

The Ivy-Tower Architects have the responsibility for creating the IT vision for the company or departments they are rarely accountable for their decisions. If, for some reason, something goes wrong, they can easily say, 'I gave clear guidelines.' Usually, these guidelines are a few Powerpoint presentations or diagrams from Microsoft Vision, links from the Internet, or small pocs that don't reflect the reality faced by developers. 'We should probably hire better developers. They can't understand the one problem in memory-data grid I use. It's written on the website that many companies use this product. It must be good.' With a closer relationship to the business, and being able to use the developers as scapegoats when things go wrong, Ivy-Tower Architects responsible for the solution the developers are the ones who are accountable for it. Maybe, in the example above, the application built by the developer never needed an in-memory data grid.

Although we always push for productive conversations, some Ivory-Tower Architects are not open to that. They see developers as mere coders who should do whatever they are. But one way to get our point across is to acknowledge architects for decisions. If we have no say in the technical solution, then it is fair that we are not held accountable for it. Passive-aggressive is a last-resort measure.

Once, while I was working for a large organization, the relationship between the team and the Ivy-Tower Architect I dealt with for months was tense, unnecessary complexity, frustration, and loads of arguments, here is a conversation with the Ivy-tower Architects.

> "Who authorized your code base this framework? Why are you not using the one I recommended?

> "Because the other web framework is not a good fit for our project. Also, I didn't Know your authorization for choosing a framework. I thought the development team was responsible for that," I said.

> "Who do you think I'm here for? This which frameworks and libraries are used in all the projects."

> "Ah"

> "I'm responsible for the technical solution. From the vision to the implementation, including frameworks and libraries."

> "Our product owner says that the business is trying to figure out what requirements are. In order to them, they decided to change the ba minimum, enabling us to change the code as fast as they want. This will provide us with a quick feedback loop and help them decide what they want."

> "How are you planning to change anything?"

> "The first thing we did was push for our continuous integration. Once our changes are merged into the repository, our continuous integration runs all the tests. If the tests pass, the application is deployed into the UAT environment. This happens multiple times a day. The business then refreshes their browsers (as many times as they want) and will see the changes. This way they can see how the system is working and making up them about what they want to change or add to it. This is one of the ways to help the business."

> "That's good, but that doesn't mean you use whatever frameworks you want. You should follow our guidelines."

> "So assume you understand all the functional and non-functional requirements of our order to prescribe the technology we use and the business itself itself."

> "I don't need to. I know the data we bought and the web framework I am recommending for all the requirements we have and should be used by everyone.",

> "That's great. But you are going to write code with us as I will? We are in a much better position to choose the tools that we make using all these tools and frameworks. However, I think that we are in making us more productive and provide a fast feedback loop to the business. The choices we are making only the internal impacts of our application and not the external world. It doesn't change how our application communicates with other applications and the legacy system."

> "Well, my role is to standardize the technology stack. This allows us to have flexibility. I had to ask what you meant. I didn't know that people could be substituted. Not everyone is a superior or inferior person. There was a moment when you forced me to make inferior."

> "People flexibility? That sense," I said with an ironic tone. You are saying that instead of choosing the right tools for the job, we should choose the tools that low-skilled developers can deal with. Instead of trying to hire better drivers or train them, the option is to back and sacrifice quality. I'll explain that to the business."

> "Sorry, that was not my intention, I probably misunderstood. Could you tell me exactly what you meant, and how a person is not directly involved in the delivery of the product which we chose the frameworks and libraries we used by the team? I don't understand how each application is in a small box of our ideas. Why exactly do you change how each box is implemented? Shouldn't you care how those boxes talk to each other, and the responsibilities they should have?"

> "Like not, like that," he said, "I get to choose the technology stack for all projects. If you want something different, you need my authorization for that. This is my responsibility."

> "OK. That's not a problem at all," I said calmly. "I go back to my desk and send an email to all the stakeholders, project managers, business analysts, and every other person involved in the project, copying you, of saying that we will be stopping the project for some time. During this time, I'll tell them that you are going to be through all Maven repository and checking if we are allowed to use all the libraries we chose. We will also be waiting for a full"
