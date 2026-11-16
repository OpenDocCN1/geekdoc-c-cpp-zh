# # Designing a Vulgarity Filtering System

Shekhar Dhupelia
sdhupelia@gmail.com

With online usernames and chat rooms more and more prevalent in recent online games, so too becomes the problem of adult content (especially when trying to ship an E-rated game). Everyone at this point would acknowledge that it's impossible to catch every possible use of vulgarity while also trying to remain efficient and user friendly. However, there are methods that will catch a lot of the more obvious cases.

This article discusses the components that go into a fast word-search vulgarity filter, including how to organize the "bad words" in a data source, how to search through all of this data, and the various options for what to do with the violating text. Also discussed are some best practices and additional points of reference when building such a system.

# ## Syntax Versus Context

It's important to keep in mind that most games cannot afford to attack the problem of "context." Context suggests the actual meaning of a sentence, or a full thought. While some standard sentences might be blocked in their entirety, a very high level of artificial intelligence would be needed to determine the meaning of a sentence and refuse potential rule violations; this is especially true since the AI would need to be running in real time.

Further, it is far beyond the scope of this gem to discuss voice chat. While it is admirable to want to provide a "family friendly" environment within a game, especially one geared towards all age levels, it is far beyond the scope of our average game hardware to monitor voice chat and do anything particularly useful with it.

The discussion here is of syntax. Syntax refers to the words themselves, while "^$%$ YOU!" still contains quite a bit of meaning, the point is that the effect is still dulled from not allowing full expletives to be transmitted back and forth.