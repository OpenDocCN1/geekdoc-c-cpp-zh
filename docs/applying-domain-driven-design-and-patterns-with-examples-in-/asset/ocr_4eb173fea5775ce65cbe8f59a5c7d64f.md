Now you can add more rules during instantiation of Domain Model classes, but as I said instantiation gets a bit messy, and you should probably use a Factory of some sort.

The good news is that the customization we just talked about works seam-lessly with the possibility of dragging out information about the rules, which comes in very handy for creating the forms.

# Providing the Consumer with Metadata

The persistence related rules should be treated as something that can be dragged out of the Domain Model instance proactively. This is because they could be easily used by the consumer. I add another method to the IValidatableRegardingPersistence interface:

```
interface IValidatableRegardingPersistence
{
    bool IsValidRegardingPersistence {get;}
    IList BrokenRulesRegardingPersistence {get;}
    IList PersistenceRelatedRules {get;}
}
```

Then it's up to the consumer to do something interesting with the rules she finds. There will probably be some rules that are easily used by the UI when new forms are shown, such as fields that are required, certain value ranges, lengths of strings and so on.

Conceptually, I like the solution. Something like this should be useful for a great number of projects. But I can't help feeling that it is still a bit smelly, especially regarding the transition-specific rules, at least if the scale of the problem increases.

# A Problem Suitable for a Pattern?

What do you think about using the State pattern [GoF Design Patterns] here? We discussed it quite a lot in Chapter 2, “A Head Start on Patterns.” It’s quite appealing if you ask me, and it means I can delegate the responsibility of the transition-specific lists out into the certain state classes. It’s actually a problem that the State pattern is pretty much made for.

You can also work with several levels in the inheritance hierarchy regarding the different states; for example, if an instance-based rule definition is the same for several of the states.

# What About the Complex Rules?

As I said, I don’t mind writing the complex rules by hand. I want to spend my time there.

I think applying the Specification pattern [Evans DDD] is often a good idea for complex rules.

What we try to achieve when using Specifications is to express important domain concepts in code. The common theme with DDD is to be concept-focused. (The focus is on domain concepts instead of just technical concepts. For example, numeric intervals and string lengths are more of technical