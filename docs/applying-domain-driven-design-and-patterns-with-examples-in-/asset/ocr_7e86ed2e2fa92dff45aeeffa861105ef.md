# Binding to the Persistence Abstraction

In the previous chapter, I talked about how to prepare for the persistence infrastructure by working with an abstraction layer that I called NWorkspace (which is just an example of such an abstraction of course). As you might have guessed, it has some support for validation as well, because the reactive nature needs to be dealt with when we make calls to PersistAll().

Of course, I don't want the persistence abstraction to expect a certain interface to be implemented on the Aggregate roots.

# Make the Validation Interface Pluggable

Therefore, I made it possible to inject an IValidator to the IWorkspace. The IValidator interface looks like this:

```
public interface IValidator
{
    bool IsValidatable(object entity);
    bool IsValid(object entity);
    IList BrokenRules(object entity);
}
```

The IWorkspace implementation talks to the IValidator implementation, and the IValidator implementation then decides what interfaces to look for on the entities. In my case, the IValidator implementation looks for IValidatableRegardingPersistence implementations and knows what to do with the IValidatableRegardingPersistence implementation in order to throw an exception during PersistAll(), if necessary. To make this a bit more concrete, see Figure 7-3.

Figure 7-3. Overview of the collaborating pieces

![](bbox=[0.25, 0.9, 0.75, 0.98])