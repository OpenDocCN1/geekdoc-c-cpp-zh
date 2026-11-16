
and link time, the compiler will choose the overloaded function calls over the standard library calls.

Overloading standard C calls to rand() is as simple as:

```
#define rand() Pools::getRandomNumber(POOL_DEFAULT)
```

Also, a good way of tracking down the engineer responsible for misused rand() and srand() calls is to trap any calls to standard srand() as well:

```
#define srand(x) Pools::seedPools(x)
```

Making sure that the random pools header is available via #include high up in the compilation/link hierarchy, or is listed in a precompiled header, is usually all it takes to propagate these macros.

## Next Steps: Logging and Debugging

Once the random pool system is in place, it can itself become a powerful debugging tool for online game issues. This is particularly true in deterministic games, where game state must remain completely in lockstep for the duration of the session.

A good method in finding problems between desynchronized machines is by comparing the usage of the random pools on each system. Implementing logging of function calls to getRandomNumber() should be fairly trivial (depending on the platform), and comparing the output from each machine should help isolate some of the application code problems leading to “out-of-syncs.”

## Next Steps: Instant Replay

On top of just providing extra logging and debugging, for some games, the random pools class can actually form the basis for an Instant Replay feature! Instead of recording game state frame-by-frame, simply record the results of calls to getRandomNumber() along with controller/keyboard/mouse input. This data should be stored in precise sequential order. These values can then be used to essentially “replay” a frame at any given point, feeding the same inputs back into all the various subsystems at work. While these other systems are oblivious to what’s going on, and are essentially re-doing the same work, this data set is very small and economical. This is a benefit even for many offline games.

## Conclusion

This gem discussed multiple uses for a random number pool system. Chief among these is the ease in which networked games can be synchronized; this makes sure that a request for a random number comes up with the same result on every machine. In addition, random numbers controlled by the application allows a programmer to replay various subsystems over and over again, either as a debugging tool or as an actual feature of the game.

## References

[Isensee01] Isensee, Pete. “Genuine Random Number Generation.” Game Programming Gems 2. Charles River Media, 2001.

[Thomas01] Thomas, Andy. “Randomal64 Pseudo Random Number Generator.” Available online at http://www.generation5.org/content/2001/fga01.asp.

## 6.8 Secure by Design

Adam Martin, Grex Games

gpg@grexengine.com

A system is only as secure as its weakest link, so spending time and money on securing only some aspects of a system is usually a pointless waste. You must check every single link to have any confidence in your security, and yet most project leads do not even know what links they have, let alone how to evaluate them.

The ability to evaluate security is critical for any multiplayer or online game, yet the modern software engineer seems to fix problems in the completion and a post-release evaluation phases rather than during design phase. We need to design security into our games from the very start.

This gem describes a multistage process that can easily be integrated with your existing development processes. Ideally, you would follow this process from the start of your project, but it is still extremely effective when applied retroactively. The text and examples concentrate on securing servers in particular, but the process itself is equally applicable to client activities.

We work from the basis that an insecure system is formally defined as one where one or more attacks from the actual Threat Model (TM) are not dealt with by the actual Security Policy (SP). If we produce a complete TM and fully adhere to our own SP, we can calculate how secure our system is simply by looking at these two documents. This is the major aim of this gem. This is a simplified view of a concept known formally as a Security Target.

The TM and the SP together fully document the system's weaknesses, its solutions, and enough information to quickly reproduce and re-evaluate the original assumptions and conclusions.

### How Important Is Security, Really?

Security flaws tend to be like software bugs in that the cost of fixing them rises exponentially the longer it takes to discover them. However, security flaws tend to rise in cost even faster than normal bugs. For instance, the cost of a flaw that exposes the credit card details of all your subscribers is astronomical compared to the cost of fixing it before going live.

Most people associate security primarily with encryption, passwords, and authentication schemes, but these are merely tools, and do not constitute security themselves. There are currently three main approaches to game security in a wider sense:

- Wait until release, see what breaks, then desperately issue patches as quickly as possible.
- Delegate to someone else (person or company) and hope they are sufficiently afraid of being blamed that they somehow work out how to secure the system.
- Deploy a suite of known tactics in haphazard fashion, hoping you might just manage to make it “a bit more difficult to hack.”

In almost all cases, it is extremely expensive—and difficult—to fix security late in the development process. The received wisdom is that security cannot be added retroactively, because it is simply too expensive; it needs to be “designed in from the start.” If your development process failed to take proper account of security concerns, you risk being condemned to producing a never-ending stream of security patches, none of which ever completely fix the problems, while “grief players” run amok in your multiplayer game, ruining it for your other players, leading to poor reviews and reducing sales.

On the other hand, perhaps your game is a Massively Multiplayer Online Game (MMOG), and as your game world falls to pieces under the grief-players, subscribers start canceling in large numbers. Worse, one of those holes might expose your per-customer credit-card details, taking the financial and reputation damage to completely new levels. Anything you own or control—data, hardware, bandwidth, even your company’s identity—could easily be abused or stolen if your game-server security is inadequate.

Fortunately, the process in this gem is both simple and cheap, and produces benefits right from the start. Every game developer—from professional studios to individual hobbyists—should be able to use this process easily and effectively.

## Aims

As [Schneier03] points out, “security” is basically meaningless unless you know from whom and for how long it is secure. Therefore, our first aim is to formalize exactly what we mean; this is a process that needs to be performed separately for each project; there is no single answer for every game.

Assuming we know what we are trying to protect, we also need a way of measuring our success. Developers today are accustomed to using metrics to assess code improvements in the development phases of a project: bug lists, unit tests, playable demos, etc. We need an equivalent for security, that is, we need a precise measure of “secureness.”

Then there is the problem of cost: if every game project had infinite time and an infinite budget, it could simply be written very carefully and be penetration-tested extensively. Nevertheless, assuming we have limits on our resources, we need to be able to prioritize where to spend them. We also need to be able to make predictive measures of “secureness” and compare them to each other (e.g., so that we can decide which of two designs to implement). Therefore, another aim is comparability.

Both of the aims also require that results are easily repeatable, not just by the original measurers, but by other people, too. We cannot make the process entirely repeatable, since one aspect of security—the discovery of attacks on a system—is inherently creative rather than methodical, and so there will always be an element of non-determinism. It would be helpful if this non-determinism could be strictly limited in some way.

It is generally too expensive to reassess the entire system for each alternative, and so we need some way of restricting our comparisons. The ideal solution would be some form of encapsulated measurements, so that we only need to remeasure the parts of the system that are changed.

## Terminology

Unfortunately, the security industry lags behind software engineering in terms of both formalization and standardization. Until greater formalization is achieved, there continue to be many self-proclaimed experts whose teachings are variable at best and often promote positively dangerous approaches to security; in this environment, it is particularly difficult to know whom to trust as an authority. Until the industry standardizes more widely, most terminology has no single strict definition. This gem attempts to adhere to the most mainstream terminology, but in many cases there is no clear leader.

In particular, many sources define “Security Policy” in wildly differing ways. The version used by this gem is an augmented version of one of the most common definitions. Some sources are passionately contemptuous of that base definition, declaiming, “Policies are not technical manuals.” For CIOs running large corporations, there is a document that they describe that has its own value; it is mainly for giving to non-technical staff as a series of daily rules to post next to their workstations, usually just one sheet of A4 that every staff member can memorize. Unfortunately, this document is usually also known as a Security Policy, and has led to some confusion, with a significant number of people coming to believe that this is sufficient to provide security. While it is another one of those useful tools in the over-arching process, it does not provide the core features of repeatability and completeness that our Security Policy does provide.

## Threat Model: Measuring Insecurity

[Berg02] states that the first step is to create a method to quantify and evaluate risk. We start with the Threat Model (TM), which models the inherent risks. We then use this to produce a Security Policy (SP), which explains how we deal with them.
