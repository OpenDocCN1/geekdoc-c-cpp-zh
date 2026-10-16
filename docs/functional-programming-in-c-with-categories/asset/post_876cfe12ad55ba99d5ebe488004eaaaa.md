
```
public T Value { get; set; }
public Id(T value) => Value = value;

public T1 MatchWith<T1>(Func<T, T1> callback) => callback(Value);
public void MatchWith(Action<T> callback) => callback(Value);
}
```

![](img/d73681d801b4b826e0b2a293897bbba4_118_0.png)

```
new Id<int>(3).MatchWith(Console.WriteLine);
```

```
Console.WriteLine( new Id<int>(3).value)    // Instead of this
```

If we want to get just the value we can pass the identity function inside

```
var value =new Id<int>(3).MatchWith (x=>x);
```

here we are going to use the for the first time the C#8.0 pattern matching in a trivial way.
Take a look :

```
string result = new Id<int>(5)
    switch
    {
        Id<int> { Value: var v } => v.ToString(),
    };
```

Using the following switch syntax:

```
switch
{
    _ =>
};
```

We can peak inside the Id<int>( )

```
switch
{
    Id<int> { } => _
};
```

and match the value (access the value, make a claim about how the Id<int>( ) looks if dissected)

```
switch
{
    Id<int> { Value: var v } => _
};
```

In some pure Functional language this could look like this :

**Id(5) = Id(x)**

And immediately the x inferred as a 5 because the left side must match as a pattern the right side. The C# syntax is more verbose.

## Pattern match over Composition

Let us add another Property inside Id and Make it into a Pair “container” (basically that is a custom Tuple)

```
public class Pair<T>
{
    public T Value1 { get; set; }
    public T Value2 { get; set; }
    public Pair(T value1, T value2) { Value1 = value1; Value2 = value2; }
    public Pair<T1> Map<T1>(Func<T,T1> f) =>new Pair<T1>(f(Value1),f(Value2));
}
```

we can define MatchWith as:

```
public T1 MatchWith<T1>(Func<T, T, T1> callback) =>
    callback(Value1, Value2);
```

this is just an Object-oriented composition of Value1 and Value2, or in other interpretation a product type of Value1 and Value2. We can use now the MatchWith to extract the values:

```
string pairResult1 = new Pair<int>(4, 5)
    .MatchWith((v1, v2) => (v1 + v2).ToString());
```

## Using C# 8.0 pattern matching

If we use the native syntax this becomes :

```
string pairResult = new Pair<int>(4,5)
    switch
    {
        Pair<int> { Value1: var v1, Value2:var v2} => (v1+v2).ToString(),
    };
```

Run This: .Net Fiddle

## Pattern match over Inheritance

Let us say now that you we have a simple hierarchy of shapes:

```
abstract class Shape { }
```

```
class Rectangle : Shape
{
    public int Width { get; set; }
    public int Height { get; set; }
}

class Circle : Shape
{
    public int Radius { get; set; }
}
```

Now if i make an assignment to a Shape variable . I can assign either a rectangle or a circle. Here i will go with the rectangle:

```
Shape shape = new Rectangle { Width = 100, Height = 100, };
```

How can you find out during runtime what kind of shape did i put in ? Use pattern matching of course. From the inheritance perspective usually, we use words like case analysis.

We can go with the traditional usage of switch since C# 7.0

```
string GetShapeDescription(Shape shape)
{
    switch (shape)
    {
        case Circle c:
            return $"found a circle with radius {c.Radius}";
        case Rectangle s:
            return $"Found {s.Height }x {s.Width} rectangle";
        default:
            throw new System.Exception(nameof(shape));
    }
};
```

Great but in the same spirit with the previous section we can define a MatchWith that take some Callbacks that expose the values:

```
abstract class Shape
{
    public abstract T MatchWith<T>(Func<Rectangle, T> rectangleCase,
        Func<Circle, T> circleCase);
}
```

```
class Rectangle : Shape
{
    public int Width { get; set; }
    public int Height { get; set; }

    public override T MatchWith<T>(Func<Rectangle, T> rectangleCase,
```

```
Func<Circle, T> circleCase)
=> rectangleCase(this);
```

```
}

class Circle : Shape
{
    public int Radius { get; set; }
    public override T MatchWith<T>(Func<Rectangle, T> rectangleCase,
        Func<Circle, T> circleCase)
        => circleCase(this);
}
```

Which we can use like this:

```
Shape shape = new Rectangle { Width = 100, Height = 100, };
```

```
var description = shape.MatchWith<string>(
    rectangleCase: r => $"Found {r.Height}x {r.Width} rectangle",
    circleCase: c => $"found a circle with radius {c.Radius}"
);
```

## Using C# 8.0 pattern matching

As you can imagine we can write the same in C#8.0 finally without having to create custom pattern matching definitions like this:

```
string GetShapeDescription(Shape shape) =>
    shape switch
    {
        Rectangle { Height: var h,Width: var w } => $"Found {h }x {w} rectangle",
        Circle { Radius: var r } => $"found a circle with radius {r}",
    };
```

And use it like this:

```
Shape shape = new Rectangle{Width = 100, Height = 100,};
```

```
var description = GetShapeDescription(shape);
```

We are going to see pattern matching in many Functors that have an Inheritance structure.

## 4.5 Id<T> Functor on the Fly

We can use extension methods to allow the creation an Id<T> from a value T and use the Map immediately and then Fold.

```
public static Id<T> ToId<T>(this T @this) => new Id<T>(@this);
```

And thus write:

```
(5).ToId()
.Map(x => x + 1)
.MatchWith(Console.WriteLine);
```

Is this useful? maybe, maybe not. but it signifies a way of writing that is very common in Functional programming using chaining and using transformation methods like .ToId() In order to move from one data structure into another.

The Id<T> and the T are isomorphic. They contain the exact same information and thus we can go back and forth without losing any information or needing any additional information by using the methods ToId<T> and Fold() (which are inverses in a sense)

![](img/d73681d801b4b826e0b2a293897bbba4_122_0.png)

throughout this book we will see many isomorphisms. Those isomorphisms in the case of Functors are called Natural Transformations. We will see them in more detail in a latter chapter. For now, we are going to see four more isomorphisms (Task, Func, Lazy, IO) with the plain value T and thus provide you with a unifying abstraction when dealing with them.

### 4.5.1 Some more Isomorphisms

But first lats create another functor related to T. The value just T can be seen as a List with only one element:

```
public static List<T> ToList<T>(this T @this) => new List<T> { @this };
```

its inverse is the First() since for example 5.ToList().First()==5;

![](img/d73681d801b4b826e0b2a293897bbba4_122_1.png)

T also is a ValueTuple with one element

```
ValueTuple<int> t1 = ValueTuple.Create(5);
```

Which has as its inverse the generic Fold implementation by Microsoft for Tuples:

```
static S Fold<A, S>(this System.ValueTuple<A> self, S state, System.Func<S, A, S> fold);
```

this is the standard Fold signature which is the equivalent of the List.Aggregate and we can use it to get the value back like this:

```
var value = t1.Fold(0, (a, e) => a + e);
```

![](img/d73681d801b4b826e0b2a293897bbba4_123_0.png)

Finally, obviously ValueTuple<T> isomorphic to List<T> so we can create some extension methods to go from one to the other

```
static List<T> ToList<T>(this ValueTuple<T, T> @this) => new List<T> {
    @this.Item1,
    @this.Item2
};
```

ValueTuple is a Functor since is equivalent with the List () but just for fun we can create a ValueTuple .Map extension method directly :

```
static ValueTuple<T1, T1> Map<T, T1>(this ValueTuple<T,T> @this, Func<T, T1> f) => (f(@this.Item1), f(@this.Item2));
```

## SideNote:

A very obvious observation is that if we implemented ValueTuple<T, T>.ToList<T>() and ValueTuple<T1, T1>.Map<T, T1>(f) correctly then the results of the following expressions should be equal:

```
(3, 4).ToList().Select(x => x + 4);
(3, 4).Map(x => x + 4).ToList();
```

those two expressions represent the different paths in the following diagram:

![](img/d73681d801b4b826e0b2a293897bbba4_123_1.png)
