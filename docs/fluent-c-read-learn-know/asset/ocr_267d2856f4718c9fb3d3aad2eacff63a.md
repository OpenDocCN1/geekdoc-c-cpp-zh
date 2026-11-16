# HOW'D YOU DO?

# The FontSize of the element itself

```
{Binding Source={RelativeSource Self}, Path=FontSize}
or
{Binding Source={RelativeSource Mode={x:Static RelativeSource.Self}, Path=FontSize}
```

> You'll see this syntax a lot in examples and in MSDN. Many people think it's crazier. I don't, but you can make up your own mind.

# The Width of the Window element containing the label

```
{Binding Source={RelativeSource FindAncestor, AncestorType={x:Type Window}}, Path=Width}
```

# The ActualWidth of a Grid containing the label

```
{Binding Source={RelativeSource FindAncestor, AncestorType={x:Type Grid}}, Path=ActualWidth}
```

> This was a tricky one. Did you figure out how to specify the type?