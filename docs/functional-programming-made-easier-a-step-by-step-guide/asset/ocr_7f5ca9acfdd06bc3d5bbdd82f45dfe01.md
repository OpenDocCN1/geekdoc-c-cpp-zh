```
data NoInhabitants = NoInhabitants
```

Unfortunately, this has 1 inhabitant, viz. NoInhabitants.

There is one possible solution. We can put this Type definition in a Module and then only export out the Type and NOT the Data Constructor. This way no one can construct a Void.

But there’s another, much more clever and simpler solution:

```
data Void = Void Void
```

At first glance, this may be confusing, so let’s break it down from Left to Right:

+   - The first Void is the Data Type.
+   - The second Void is the Data Constructor.
+   - The third Void is the Type Parameter to the Void Data Constructor.

So to create a Void we have to use the Void Data Constructor and pass it a Void:

```
v :: Void
v = Void (???)

```

The ??? needs to be of type Void, which we can create using the Void Data Constructor:

```
v :: Void
v = Void (Void (???))

```

But our next Data Constructor also needs a Void, which we can create using the Void Data Constructor and so on:

```
v :: Void
v = Void (Void (Void (Void (Void(Void(Void(...))))))

```

It is impossible to construct a Void since it’s only Data Constructor requires a Void. We have a chicken and egg problem.

The technical term for this is a Recursive Definition because the definition refers to itself.

Except, in this particular case, it’s an Infinitely Recursive Definition because there is no base-case to terminate the recursion.