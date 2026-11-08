
## Agile Tools

By Tim Ottinger and Jeff Langr, April 16, 2019

Makers master their tools. Carpenters become adept with hammer, measure, saw, chisel, plane, and level—all inexpensive tools—during the first steps of their career. As their needs grow, carpenters learn and employ more powerful tools (which are usually more expensive): drill, nail gun, lathe, router, CAD, and CNC to name a few.

However, master carpenters don’t abandon hand tools; they choose the right tool for the job. Using only hand tools, skilled makers can craft wood projects with higher quality and sometimes faster than with power tools. As a result, wise carpenters master their hand tools before moving on to tools that are more sophisticated. They learn the limits of the hand tools so that they know when to reach for a power tool.

Regardless of whether they use hand or power tools, carpenters always seek to master each implement they choose for their toolbox. This mastery allows them to focus on the craft itself—the delicate shaping of a high-quality piece of furniture, for example—rather than the tool. Without mastery, a tool becomes an impediment to delivery, and a poorly used tool can even cause harm to the project and its operator.

### Software Tools

Software developers must master a number of core tools:

- At least one programming language, and often more
- An integrated development environment or programmer’s editor (vim, Emacs, etc.)
- Various data formats (JSON, XML, YAML, etc.) and markup languages (including HTML)
- Command-line and script-based interaction with the operating system
- Source repository tools (Git. Is there another choice?)

*Used with permission.*

- Continuous integration/build tools (Jenkins, TeamCity, GoCD, etc.)
- Deployment/server management tools (Docker, Kubernetes, Ansible, Chef, Puppet, etc.)
- Communication tools: email, Slack, the English language (!)
- Testing tools (unit testing frameworks, Cucumber, Selenium, etc.)

These categories of tools are essential to building software. Without them, it is impossible to deliver anything in today’s world. In a sense, they represent the programmer’s toolbox of “hand tools.”

Many of these tools demand hard-earned expertise for effective use. The landscape meanwhile changes constantly, making tool mastery even more challenging. The savvy developer finds the path of least resistance and highest value through all the tools involved: what gives the biggest bang for the buck?

#### What Makes for an Effective Tool?

The tool landscape changes rapidly because we are always learning more effective ways to accomplish our goals. Witness the wide variety of source repository tools introduced in the past few decades: PVCS, ClearCase, Microsoft Visual SourceSafe, StarTeam, Perforce, CVS, Subversion, and Mercurial, to name a few. All suffered problems—too flaky, too proprietary or closed, too slow, too invasive, too scary, too complex. A winner eventually emerged, one that managed to overcome most objections: Git.

One of the most empowering aspects of Git is its ability to make you feel safe. If you were around long enough to have used one of the other tools, you likely felt a little nervous from time to time. You needed a live network connection to the server, or your work was at risk. The CVS repository would get corrupted occasionally, requiring you to muck around in its attic to hopefully uncorrupt things. The repository server crashed sometimes; even if it was backed up, you risked losing half a day’s work. Some proprietary tools suffered repository corruption, meaning you’d be on the phone for hours with support while soliciting donations for the king’s ransom needed to pay for uncorrupting it. With Subversion, you’d fear doing much branching because the more source files that were involved, the longer you’d have to wait when switching branches (we’re talking many minutes here).

A good tool should feel comfortable in your hands and not make you queasy with the dread of having to use it. Git is quick, it gives you the ability to commit locally instead of only to a server, it allows you to work from your local repository without a network connection, it handles multiple repositories and multiple branches well, and it deftly supports merges.

The interface to Git is fairly streamlined and direct. As a result, once you’ve learned Git well enough, you don’t think much about the tool itself. You instead focus on the real needs: safe storage, integration, and management of source code versions. The tool has become *transparent*.

Git is a powerful and complex tool, so just what does it mean to learn it “well enough”? Fortunately, the 80/20 rule applies: a small fraction of Git’s capabilities—20%, perhaps—gets you well over 80% of the day-to-day needs you’ll have for source management. You can learn most of what you need in minutes. The rest is available online.

The simplicity and effectiveness of using Git led to wholly unplanned, new ways of thinking about how to build software. Linus Torvalds probably would have thought it was insane to use Git as a tool to quickly throw away bits of code, but that’s exactly what proponents of the Mikado Method⁶ and TCR (Test && Commit || Revert)⁷ promote. And even though a key, powerful aspect of Git is its ability to handle branches very effectively, countless teams almost exclusively do trunk-based development while using Git. The tool is *exapted* (used effectively in ways the originators hadn’t intended).

Great tools do the following:

- Help people accomplish their objectives
- Can be learned “well enough” quickly

⁶ Ellnestam, O., and D. Broland. 2014. *The Mikado Method*. Shelter Island, NY: Manning Publications.
⁷ Beck, K. 2018. *Test && commit || revert*. Accessed at https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864.

- Become transparent to users
- Allow adaptation and exaptation
- Are affordable

We hold up Git here as an example of a great tool…as of 2019. You may be reading this in some future year, so remember that the landscape changes.

### Physical Agile Tools

Agilists are known for using whiteboards, tape, index cards, markers, and various sizes of sticky notes (small and flip-chart-size) for visual management of their work. These simple “hand implements” have all the qualities of a great tool:

- They help make work in progress visible and manageable.
- They’re intuitive—no training required!
- They require negligible cognitive overhead. You can use them easily while concentrating on other tasks.
- They’re easily exapted. None of these tools was designed expressly for managing software development.
- They’re adaptable. You can use tape or sticky putty with them, clip pictures or icons to them, tape additional indicators to them, and add nuance of meaning through novel use of custom colors and iconography.
- They’re all inexpensive and easily acquired.

Co-located teams can easily manage huge and complex projects using only these simple and inexpensive physical tools. You can radiate key information using a flip chart sheet taped to a wall. Such *information radiators* summarize important trends and facts for team members and sponsors alike. You can use these information radiators to devise and present new kinds of information on the fly. The flexibility is nearly infinite.

Every tool has its limitations. One key limitation of physical tools is that they’re not very effective for distributed teams, only for people within visual range. The physical tools also don’t automatically maintain history—you have only the current state.

There’s no reason ALMs can’t be great tools someday. But if you only need to manage a card wall and must use software, adopt a general-purpose tool like Trello.<sup>8</sup> It’s easy, immediate, cheap, extensible, and won’t make you queasy.

<sup>8</sup> Again, as of 2019. The landscape changes.

Our ways of working constantly change. We evolved from SCCS to RCS to CVS to Subversion to Git over the years, tracking a sea change in the ways we managed source code. We have similar evolution in testing tools, deployment tools, and the like (not listed here). We are likely to see a similar progression in automated ALM tools.

Given the current state of most ALM tools, it may be safer and smarter to begin with physical tools. Later, you can *consider* using an ALM tool. Make sure that it’s quick to learn, transparent in daily use, easy to adapt, and within your means to acquire and run. Most importantly, ensure that it supports the way your team works and provides a positive return on your investment.

## Coaching—An Alternative View

By Damon Poole, May 14, 2019<sup>9</sup>

> *Damon Poole is a friend of mine who disagrees with me about many things. Agile coaching is just one of those things. So, I thought he’d make a good choice to provide you with a different viewpoint.*
>
> — UB

### The Many Paths to Agile

There are many paths to Agile. And in fact, many of us have walked the path unintentionally. One could argue that the Agile Manifesto was the result of the authors noticing that they were all on a similar journey and deciding to describe it such that others might choose to join them on their journey. My path to Agile started by walking into an appliance store in 1977 that happened to be selling TRS-80s. As a complete novice, I helped an

<sup>9</sup> Used with permission.
