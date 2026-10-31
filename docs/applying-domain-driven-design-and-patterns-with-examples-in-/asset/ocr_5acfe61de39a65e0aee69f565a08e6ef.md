# # A Little Bit About Patterns

Patterns provide simple, elegant solutions to recurring design problems. The key advantages patterns provide are flexibility, modularity, and creating understandable and clear design. Note that I skipped reusability, although it's a bit unfair. Patterns take away focus from code reuse and move the focus to knowledge reuse instead. So patterns are very much about reusability, too, but just not in the way we usually think about reuse.

# ## Note

Gregory Young pointed out that many patterns are about reuse, through decoupling. The Dependency Injection pattern (which will be discussed in Chapter 10, "Design Techniques to Embrace") is a good example of that.

When you study patterns, you might think "OK, isn't that how we always do it?" An important point about patterns is that they aren't invented, but rather *harvested* or *distilled*. It's about *proven* solutions. But the solution part isn't the only piece of a pattern. They are described in three pieces: the *context*, the *problem*, and the *solution*.

Learning from your mistakes is very powerful, but from time to time it's nice to take a shortcut by studying other people's amassed knowledge, which is a good reason for learning patterns. Let’s see if we can find other reasons.

# ## Why Learn About Patterns?

The most obvious reason is probably that patterns are good abstractions that provide building blocks for system design.

If a development team is patterns-conscious, patterns become a very important part of the language. Instead of having to describe each and every design idea in minute detail, it's often enough to say a pattern name and everybody in the team can evaluate whether or not it's a good idea for that particular problem. Adding patterns to the team's language might be the single most important reason for embracing patterns because the common understanding, richness, and expressiveness of the language increase. Again, development is very much about communication.

Another reason I like patterns is that being able to utilize patterns is a long-lasting skill. As a comparison, I learned SQL in around 1988, and I can still make a good living from just working with that. The products and platforms I work with have changed several times, though the underlying concepts are the same. Patterns are similar. The *Design Patterns* book [GoF Design Patterns] came out in 1995, and it's still extremely relevant today. Also worth pointing out is that patterns are language-/product-/platform-agnostic. (Different platforms might have specific