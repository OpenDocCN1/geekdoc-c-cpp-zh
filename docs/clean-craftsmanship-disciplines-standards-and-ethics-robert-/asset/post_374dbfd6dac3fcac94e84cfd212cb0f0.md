
swathes of the code use. If you were to change that data structure, those swaths would stop working and many tests would break.

Instead, you should create a new data structure that mirrors the content of the old data structure. Then, gradually, move each portion of the code from the old data structure to the new data structure while keeping the tests passing.

While this is going on, you may also be adding new features and fixing bugs according to your regular schedule of work. There is no need to ask for special time to perform this restructuring. You can keep on doing other work while you opportunistically manipulate the code until the old data structure is no longer used and can be deleted.

This may take weeks or even months, depending on how significant the restructuring is. Even so, at no time would the system be down for deployment. Even while the restructuring is only partially complete, the tests still pass and the system can be deployed into production.

## Leave Yourself an Out

When flying into an area where the weather might not be so good, pilots are taught to always make sure they leave an avenue of escape. Refactoring can be a bit like that. Sometimes you start a series of refactorings that, after an hour or two, leads you to a dead end. The idea you started with just didn’t pan out for some reason.

In situations like this, `git reset --hard` can be your friend.

So, when beginning such a sequence of refactorings, make sure to tag your source repository so you can back out if you need to.

## Conclusion

I kept this chapter intentionally brief because there were only a few ideas that I wanted to add to Martin Fowler’s *Refactoring*. Again, I urge you to refer to that book for an in-depth understanding.

The best approach to refactoring is to develop a comfortable repertoire of refactorings that you use frequently and to have a good working knowledge of many others. If you use an IDE that provides refactoring operations, make sure you understand them in detail.

Refactoring makes no sense without tests. Without tests, the opportunities for error are just too common. Even the automated refactorings that your IDE provides can sometimes make mistakes. So *always* back up your refactoring efforts with a comprehensive suite of tests.

Finally, be disciplined. Refactor frequently. Refactor mercilessly. And refactor without apology. Never, ever ask permission to refactor.

It is hard to imagine the furor this new perspective raised in the late 1990s. Designers everywhere had gotten very used to putting all the hooks in. In those days, putting the hooks in was considered conventional wisdom and a best practice.

So, when the YAGNI discipline of Extreme Programming surfaced, it was roundly criticized and panned as heresy and claptrap.

Nowadays, ironically, it is one of the most important disciplines of good software design. If you have a good suite of tests and you are skilled at the discipline of refactoring, then the cost of adding a new feature and updating the design to support that new feature will almost certainly be smaller than the cost of implementing and maintaining all the hooks you might need one day.

Hooks are problematic in any case. We seldom get them right. That’s because we are not particularly good at predicting what customers will actually do. Consequently, we tend to put in far more hooks than we need and base those hooks on assumptions that rarely pan out.

The bottom line is that the effect that gigahertz clock rates and terabyte memories had on the process of software design and architecture took us all by surprise. We did not realize until the late 1990s that those advances would allow us to vastly *simplify* our designs.

It is one of the great ironies of our industry that the exponential increase of Moore’s law that drove us to build ever-more complex software systems also made it possible to simplify the designs of those systems.

YAGNI, it turns out, is the unintended consequence of the virtually limitless computer power now at our disposal. Because our build times have shrunk down into the seconds and because we can afford to write and execute comprehensive test suites that execute in seconds, we can afford to *not* put the hooks in and instead refactor the designs as the requirements change.

Does this mean that we never put the hooks in? Do we always design our systems only for the features we need today? Do we never think ahead and plan for the future?

No, that’s not what YAGNI means. There are times when putting a particular hook in is a good idea. Future-proofing the code is not dead, and it is always wise to think of the future.

It’s just that the trade-offs have changed so dramatically in the last few decades that it is now usually better to leave the majority of the hooks out. And that’s why we ask the question:

What if you aren’t gonna need it?

## Covered by Tests

The first time I ran across Beck’s rules of simple design was in the first edition of *Extreme Programming Explained*.⁴ At that time, the four rules were as follows:

⁴. Kent Beck, *Extreme Programming Explained* (Addison-Wesley, 1999).

- 1. The system (code and tests) must communicate everything you want to communicate.
- 2. The system must contain no duplicate code.
- 3. The system should have the fewest possible classes.
- 4. The system should have the fewest possible methods.

By 2011, they had evolved to these:

- 1. Tests pass.
- 2. Reveal intent.
- 3. No duplication.
- 4. Small.

By 2014, Corey Haines had written a book⁵ about those four rules:

⁵. Corey Haines, *Understanding the Four Rules of Simple Design* (Leanpub, 2014).

In 2015, Martin Fowler wrote a blog⁶ about them in which he rephrased them:

⁶. Martin Fowler, “BeckDesignRules,” March 2, 2015, https://martinfowler.com/bliki/BeckDesignRules.xhtml.

- 1. Passes the tests.
- 2. Reveals intention.
- 3. No duplication.
- 4. Fewest elements.

In this book I express the first rule as

- 1. *Covered by tests.*

Notice how the emphasis of that first rule has changed over the years. The first rule split in two and the last two rules merged into one. Notice also that, as the years went by, tests grew in importance from communication to coverage.

### Coverage

The concept of test coverage is an old one. The first mention I was able to find goes all the way back to 1963.<sup>7</sup> The article begins with two paragraphs that I think you’ll find interesting, if not evocative.

7. Joan Miller and Clifford J Maloney, “Systematic Mistake Analysis of Digital Computer Programs,” *Communications of the ACM* 6, no. 2 (1963): 58–63.

> *Effective program checkout is imperative to any complex computer program. One or more test cases are always run for a program before it is considered ready for application to the actual problem. Each test case checks that portion of the program actually used in its computation. Too often, however, mistakes show up as late as several months (or even years) after a program has been put into operation. This is an indication that the portions of the program called upon only by rarely occurring input conditions have not been properly tested during the checkout stage.*

> *In order to rely with confidence upon any particular program it is not sufficient to know that the program works most of the time or even that it has never made a mistake so far. The real question is whether it can be counted upon to fulfill its functional specifications successfully every single time. This means that, after a program has passed the checkout stage, there should be no possibility that an unusual combination of input data or conditions may bring to light an unexpected mistake in the program. Every portion of the program must be utilized during checkout in order that its correctness be confirmed.*

Nineteen sixty-three was only seventeen years after the very first program ran on the very first electronic computer,<sup>8</sup> and already we knew that the only way to effectively mitigate the threat of software errors is to test every single line of code.

8. Presuming that the first computer was the Automated Computing Engine and that the first program executed in 1946.
