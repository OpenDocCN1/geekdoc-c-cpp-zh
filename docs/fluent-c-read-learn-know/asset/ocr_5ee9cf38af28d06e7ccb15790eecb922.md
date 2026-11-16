![](bbox=[0.11, 0.07, 0.24, 0.21])

# HOW'D YOU DO?

Are the various versions of the method starting to sort themselves out in your head?

To declare a read-only dependency property with a validation callback:

```
RegisterReadOnly(<name>, <propertyType>, <ownerType>, <PropertyMetadata>, <ValidateValueCallback>)
```

To declare an attached property with default metadata:

```
RegisterAttached(<name>, <propertyType>, <ownerType>)
```

To declare a read-only dependency property without a callback:

```
RegisterReadOnly(<name>, <propertyType>, <ownerType>, <PropertyMetadata>)
```

To declare a dependency property with the default value of false:

```
Register(<name>, <propertyType>, <ownerType>, <PropertyMetadata>)
```

To declare a read-only attached property with a validation callback:

```
Register(<name>, <propertyType>, <ownerType>, <PropertyMetadata>)
```

![](bbox=[0.11, 0.7, 0.24, 0.85])

# TAKE A BREAK

There's still a little more to learn about dependency properties, but we've covered a lot, so why don't you take a quick break before we move on to callbacks and adding owners?