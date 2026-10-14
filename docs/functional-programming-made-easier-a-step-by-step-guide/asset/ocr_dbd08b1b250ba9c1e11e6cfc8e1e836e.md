Decide which one you prefer and why. Be careful and avoid Post Rationalizing your intuitive selection, which is an easy trap to fall into.

For example, maybe we don’t like Records because we haven’t used them much and so the other model is more attractive to us. And now, to justify that SUBJECTIVE decision, we conjure up a rational, seemingly OBJECTIVE, reason for our choice. We are human and are all susceptible to this. And so it’s really important to be aware of this so that we fight against it.

So, with all of that in mind, what’s you choice and WHY? Please think about it before reading further.

Okay, now that you have your choice, I’ll tell you mine.

The way I’m going to decide is by pushing the models to their limits. Let’s imagine we have dozens and dozens of formats that we want to support. How does each model perform under those conditions?

Let’s imagine that scenario with the first model:

```
data DateParts
  = YearFirstDate Year Month Day
  | MonthFirstDate Year Month Day
  | DayFirstDate Year Month Day
  | SomeOtherFormat Year Month Day
  | AndYetAnotherFormat Year Month Day
  | SomeEsotericFormat Year Month Day
  | UghYetAnotherFormat Year Month Day
  | KillMeFormat Year Month Day
```

Notice how we had to repeat Year Month Day for all of these. Not pretty.

Let’s see how our second model performs under these same conditions: