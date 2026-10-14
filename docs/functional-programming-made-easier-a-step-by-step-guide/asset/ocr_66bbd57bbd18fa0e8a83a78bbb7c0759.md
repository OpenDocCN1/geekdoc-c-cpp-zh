And now, we’ve overcome another Technological Hurdle.

# 23.2.3. Creating a `Fiber`

Although we’ve done this in the previous Chapter, it’s possible you’ve already forgotten how to do this. One way to refresh your memory is to reread the previous Chapter.

Another way is to look at the last bit of code we wrote in that Chapter. Since the latter is far simpler, take the time now to turn back and look at the last program we wrote at the very end of the previous Chapter to see how we create a `Fiber`.

Return here once you’ve found it.

Okay, so I’m going to assume you looked and you either found out how to create a `Fiber` or came up short. If you figured it out, great, but pretend, for just a moment, that you did not.

Let’s say, you know you want to create an Asynchronous Process but you don’t know how. But you do know about the module `Effect.Aff`. Look that module up on `Pursuit` and browse the module’s documentation for a Function that will create a new `Fiber`.

Try it and see what you find.

When I do this, the first thing I encounter is `launchAff`:

```
launchAff :: ∀ a. Aff a → Effect (Fiber a)
```

This takes code written in the `Aff` Monad and returns the `Fiber`. Note that this runs in the `Effect` Monad. So, it’s good for running a `Fiber` from inside our `main` or, in our case throughout this book, inside our test code.

But what if we’re not in `Effect`. What if we’re in `Aff` and we’d like to create another `Fiber`?

Search the page for `Aff a → Aff (Fiber a)` and then continue on.

When I do this, I find:

```
forkAff :: ∀ a. Aff a → Aff (Fiber a)
```

This is the `Aff` equivalent of `launchAff`.

So, now we know how to create a `Fiber` in either `Effect` or `Aff`. We have now knocked down another Technological Hurdle.