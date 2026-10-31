Patterns are not only great with up-front design, they are very usable (perhaps even more) during refactoring... *"My code is just becoming messier and messier. Ah, I need to use that pattern!"* It's like the chicken or the egg problem, but I decided to start with patterns in this book and discuss refactoring after that (in the next chapter).

# Is There Something to Look Out for Regarding Patterns?

Honestly, I see little reason for not learning about patterns, but there is at least one very common negative effect to look out for. What I'm thinking about is that for developers who have just learned about patterns, it's very common that they feel compelled to squeeze in 17 patterns in each and every solution. Most often that effect won't stay around for very long.

What might stay around for a little longer is the risk of over-design. If not 17 patterns, there might at least be a lot of thought about how a problem should be solved. The initial solution doesn't feel right because it doesn't use a certain pattern.

# Note

A friend of mine told me about a recent design problem he discussed with some developers at a company. It took him three minutes to come up with a very simple solution to the problem. (The problem itself was a simple one.) Yet the other developers weren't happy with the solution so they spent three days of hard thinking to get it just right.

Been there, done that. In my opinion, *Test-Driven Development* (TDD) is a good technique for avoiding that over-design problem. The design focus will be much more on solving the problem at hand and nothing else, and patterns will be introduced when needed via refactoring.

You might get the feeling that the patterns concept is the silver bullet. It's not of course not it's just another tool for the toolbox.

Patterns are often perceived individually as being pretty "simple," but they get very complex in context and combination with other patterns. I don't remember how many times I've heard people on the newsgroups say something like "I understand pattern X, but when I try to use it in my application together with pattern Y and pattern Z, it's extremely complex. Please help!" That isn't really a reason not to learn about patterns. This book will address that to some degree, but not here and now; first we will discuss some patterns in isolation.

I believe Joshua Kerievsky's *Refactoring to Patterns* [Kerievsky R2P] sets this straight by pointing out again and again that the way to most often use patterns isn't to use them in up-front design, but to refactor toward or to patterns.