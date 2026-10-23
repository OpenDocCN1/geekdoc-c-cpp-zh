```
void execute(double S) override
{ // Iterate over each element of the composite and call
    // its execute()

    for (auto it = data.begin(); it != data.end(); ++it)
    {
        (*it)->execute(S); // nested pointer
    }
};
```

This class supports the creation of trees of option commands to any level of nesting. It is a special case of the Composite design pattern (GOF, 1995). The implementation can also be generalised to one that is a generic composite using shared pointers (Demming and Duffy, 2010). In other words, you can apply the Command pattern in new applications and “use the solution a million times over without ever doing it the same way twice” (Alexander, 1979).

We take our first example of a composite command:

```
void TestCompositeCommand()
{ // Create a composite option command

    double K = 65.0;
    double T = 0.25;
    double r = 0.08;
    double b = r;
    double sig = 0.3;

    double S = 60.0;

    // Create composite command
    std::cout << "Command on options\n";
    CompositeCommand optionCommand;

    // Add prices and their deltas
    optionCommand.add(new CallPrice(K, T, r, b, sig));
    optionCommand.add(new PutPrice(K, T, r, b, sig));

    optionCommand.add(new CallDelta(K, T, r, b, sig));
    optionCommand.add(new PutDelta(K, T, r, b, sig));

    std::cout << "Size of commandlist: "
              << optionCommand.size();
    optionCommand.execute(S);
}
```

The output produced is:

```
Command on options
Size of commandlist: 4
```