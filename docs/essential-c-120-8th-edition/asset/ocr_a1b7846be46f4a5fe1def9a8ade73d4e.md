```
remove{
  remove_OnTemperatureChange(value);
}
#endif // ConceptualEquivalentCode
```

In other words, the code shown in Listing 14.15 is (conceptually) the C# shorthand that the compiler uses to trigger the code expansion shown in Listing 14.16. (The "conceptually" qualifier is needed because some details regarding thread synchronization have been eliminated for elucidation.)

The C# compiler first parses the original event definition and defines a private delegate in its place. As a result, the delegate becomes unavailable to any external class—even derived from it.

Next, the C# compiler defines two methods, add_OnTemperatureChange() and remove_OnTemperatureChange(), in which the OnTemperature suffix is taken from the original name of the event. These methods are responsible for implementing += and -= assignment operators, respectively. As Listing 14.16 shows, these methods are implemented using the static System.Delegate.Combine() and System.Delegate.Remove() methods, discussed earlier in the chapter. The first parameter passed to each of these methods is the private EventHandler<TemperatureArgs> delegate instance, OnTemperatureChange.

Perhaps the most curious part of the generated code for the event keyword is the last segment. The syntax is very similar to that of a property's getter and setter methods, except that the methods are called add and remove, respectively. The add block takes care of handling the += operator by passing the call to add_OnTemperatureChange(). In a similar manner, the remove block operator handles the -= by passing the call on remove_OnTemperatureChange.

Take careful note of the similarities between this code and the code generated for a property. Recall that the C# implementation of a property is to create get_<propertyName> and set_<propertyName> and then to pass calls to the get and set blocks on these methods. Clearly, the syntax in such cases is very similar.