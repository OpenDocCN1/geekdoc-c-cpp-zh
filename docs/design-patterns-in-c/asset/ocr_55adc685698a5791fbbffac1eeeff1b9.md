```
settingsClone.ApplicationSettings = "NewSettings"; // Change property
Console.WriteLine("INSTANCE 1: " + settings.ToString());
Console.WriteLine("INSTANCE 2: " + settingsClone.ToString());
Console.ReadKey(false);
}
```

On executing the application we can see the following results.

![](bbox=[0.18, 0.235, 0.898, 0.51])

We can see from the above code that:

+   1. Instance 1 was created using new keyword
+   2. Instance 2 was created using Clone() method
+   3. Changing of Instance 2 does not affect Instance 1

So this concludes our experiment with the Prototype pattern.

# References

http://sourcemaking.com/design_patterns/prototype

# Summary

In this chapter we have explored the Prototype pattern. The usage of Prototype pattern can be summarized as:

+   - Faster instance creation with required properties
+   - The new keyword can be avoided in instance creation
+   - Provides an alternative to Abstract Factory pattern
+   - Runtime specification of instance properties