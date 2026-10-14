+   - How to create a Bus
+   - How to Publish to a Bus
+   - How to Subscribe to a Bus

Hopefully, I’ve listed all of the things on your list. Don’t worry if not since we’re going to go over every piece of how to write this.

The whole point of making a list of Technological Hurdles is to give us a list of things that we must solve before we can ever hope to write the program at hand. Once we’ve conquered this list, writing the program is a foregone conclusion and should be pretty easy.

# 23.2.1. Creating a Random Number

How do we create a Random Number?

How would you go about figuring this out if you weren’t reading this book?

There are 2 ways that pops to mind. First, use Google. The problem with this approach is PureScript is pretty obscure and I wouldn’t expect there to be a StackOverflow question that answers this for us.

At the time of this writing, a Google search produces no such easy answers. Give it a try and see if the world has changed.

The next approach is to search Pursuit for the word random. When I do this, I’m hoping that I’ll find some Function with that name. Before reading further do this search for yourself and see if you have any luck.

This approach doesn’t always work, especially when you guess the wrong word for the Function. Luckily though, there aren’t too many synonyms for random. When we search for random, we find that the Function we’re looking for is first in the list:

```
import Effect.Random (random)

random :: Effect Number
```

Can you see a problem with this Function? If not, go back and reread the specifications.

The problem is that random runs in the Effect Monad but the specifications says that we’re going to have 3 Publishers each running in their own Fiber.

But from last Chapter, we learned that Fibers run in Aff not Effect. So how do we solve this problem?

We could find a version of random that runs in Aff. So, go look for one and see if you can find it.

Turns out, there isn’t one.

So, now what?