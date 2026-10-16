
thus, the diagram must commute. This is the hallmark of a valid isomorphism between Functors the structure should be preserved after the Map and Iso transformations.

## 4.5.2 The Basic Functor Mechanics

The following picture represents the whole idea behind how we construct the map of a functor. If we accept the Functor as a container metaphor, which is an acceptable way to visualize functors especially in an Object-oriented programming setting.

![](img/d73681d801b4b826e0b2a293897bbba4_124_0.png)

The mapping function that lifts the function f: int → int It follows the steps:

- 1. Open the container F(a) and access the value a
- 2. Applying the function f on the value a and get a new value b
- 3. wraps the resulting value again into a new container F(b) and return this F(b)

in the simplest form of the Identity functor the map follows those steps

```
public class Id<T>
{
	public T Value { get; set; }
	public Id(T value)= Value = value;
	public Id<T> Map<T>(Func<T, T> f) => new Id<T>(f(Value));
}
```

## 4.6 Extending Task<T> to Functor

In the following sections, we will see some examples of other popular Functors in C#. We will start by extending Task<T>, by providing a Map method that obeys the functor laws and thus promote native Task<T> into a functor.

We have said that the usual metaphor for a functor is “a container.” A Task can be seen as a container that takes a value and wraps it, until it is resolved. In order to promote Task<T> to Functor, there must be a mapping function that would be able to lift any function and give a new Task<T> with the lifted value.

Here is one possible mapping function that preserves structure:

```
public static Task<T1> Map<T, T1>(this Task<T> task, Func<T, T1> mapping)
{
    var value = task.GetAwaiter().GetResult();
    return Task<T1>.Run(() => mapping(value));
}
```

```
Task<int>task2 = Task<int>.Run(() => 2).Map(x => x * x);
```

Run This: .Net Fiddle

The mapping function that lifts the function f: T → T1 It follows the steps:

- 4. Waits for the result of the Task (so in a way unwraps the contained value) task.GetAwaiter().GetResult()
- 5. Applying the function f : f(value)
- 6. wraps the resulting value again into a new Task: Task<T1>.Run(() => f(value)); because when we implement a Map, we always return something of the same type in order to belong to the same category (in this case type) or Promise.

Keep those steps in mind because they are common in the implementation of many Functors and monads.

SideNote : From now on we will write the Task<T> Map Method in this way

```
public static Task<T1> Select<T, T1>(this Task<T> task, Func<T, T1> mapping)=>
    task.ContinueWith(t => mapping(t.Result));
```

where we will utilize the ContinueWith do continue the task.

> Something worth pointing out here is the possibility of exception this part belongs to the path of failure and ignores the f mapping (one could argue that if there is an exception then this does not behave like a functor we will deal with this issue when we talk about the Either functor) We are going to come back to this observation many times throughout this book.

We can use our map function now:

## 4.7 IO Functor, a Lazy Id Functor

Another simple functor which extends the identity functor by adding Laziness is the IO functor. The IO is a lazy Id functor. IO comes handy when we want to Objectify a function, pass it around and use it later to produce a side effect as we will see.Lazy<T> as Functor

```
public static Lazy<T1> Map<T, T1>(this Lazy<T> @this, Func<T, T1> f) =>
new Lazy<T1>(() => f(@this.Value));
```

The mechanics behind the mapping function that lifts the function f: T →T1 follows the same stapes as Task<T>:

- 1. Waits for the result of the Lazy (so in a way unwraps the contained value) @this.Value
- 2. Applying the function f : f(@this.Value)
- 3. wraps the resulting value again into a new Lazy: Lazy<T1>(() => f(@this.Value)) because when we implement a Map, we always return something of the same type in order to belong to the same category (in this case type).

You must appreciate that this preserves the Laziness of the Lazy<T> at no point the Lazy must collapse without trying to access the outer Value. At the step 3 we apply a lazy wrapper() => around what seems like an evaluation,@this.Value, and thus is not executed.

### 4.7.1 Func<T> Delegates as Functor

We can similarly extend the Func<T> delegate in order to provide a Map method:

```
public static Func<T1> Map<T, T1>(this Func<T> @this, Func<T, T1> f) =>
new Func<T1>(() => f(@this()));
```

By now you probably have figure out a pattern between The Task, Lazy and Func implementation of a Map. The map is a powerful abstraction over the specific mechanics of each type. Map abstracts over the need to transform the value inside a data structure.

### 4.7.2 IO Functor

Functional programming in the same lines provides the IO functor:

```
public class IO<T>
{
    public Func<T> Fn { get; set; }
    public IO(Func<T> fn) => Fn = fn;
    public IO<T1> Map<T1>(Func<T, T1> f) => new IO<T1>(() => f(Fn()));
    public T1 MatchWith<T1>(Func<T, T1> callback) => callback(Fn());
    public T Run() => Fn();
}
```

And use it in this way:

```
new IO<int>(() => 3)
    .Map(x => x + 3)
    .MatchWith(Console.WriteLine);
```

Run This: .Net Fiddle

![](img/d73681d801b4b826e0b2a293897bbba4_128_0.png)

the map implementation should remind you slightly of the Task Map line of reasoning while implementing it.

- 1. We first have to “run” the previous computation Fn()
- 2. Then use the function f to get the lifted value f(Fn())
- 3. And then finally rewrap this new value in a new new IO<T1>(() => f(Fn())).

![](img/d73681d801b4b826e0b2a293897bbba4_128_1.png)

An example application would be to use an IO, to isolate the effects of accessing the Console. This is considered **Side effect** because there is no predictability on the Input. It is not *Referential Transparent*.

```
var readKeyInstruction = new IO<ConsoleKeyInfo>(() => Console.ReadKey());
```

```
var UserInputAsInt = readKeyInstruction
    .Map(x => int.Parse(x.KeyChar.ToString()))
    .Run();
```

Run This: .Net Fiddle

It’s the same as the Id functor but encloses the value that we provide in a thunk - () => { } just to make it lazy. We would have to collapse the function Fn() in order to get back the value, most IO implementations around usually provide a Run() function that does just that. Also, with an extension method, we can create IOs out of everything on the fly.

```
public static IO<T> ToIO<T>(this T @this) => new IO<T>(() => @this);
```

## 4.8 Reader Functor

The Reader Functor represents a computation, which can read values from a shared environment. The reader functor conceptualizes the idea of having stored expression that we can evaluate in different configurations at a later time. We can represent this like that ((→) env), which means we give an environment, and we get out the thing that we want.

```
public class Reader<Env, T>
{
    public Func<Env, T> Fn { get; set; }
    public Reader(Func<Env, T> fn) => Fn = fn;
    public Reader<Env, T1> Map<T1>(Func<T, T1> f) =>
        new Reader<Env, T1>((env) => f(Fn(env)));
    public T Run(Env env) => Fn(env);
}
```

![](img/d73681d801b4b826e0b2a293897bbba4_129_0.png)

For a simple example we might have a Config type that contains various parameters and we want to create a Reader that stores a simple expression that depends on the

Config. With the reader we can do computations on the expression Lazily without having the Config yet:

```
public class Config
{
    public string Name { get; set; }
}
```

```
var getName = new Reader<Config, string>(environment => environment.Name).
    Map(name => $"Name: {name }").
    Run(new Config { Name = "Sql" });
```

the map here takes a function (a → b) and then lifts the initial reader that contains an a (((→) e) a) to a reader that contains a b (((→) e) b)

map: (a → b) → (((→) e) a) → (((→) e) b)

the implementation is more convoluted but again follows the lines of Task<T> and IO

- 1. First, we evaluate the inner reader Fn(env) (so in a way unwraps the contained value)
- 2. Applying the function f: f(Fn(env))
- 3. wraps the resulting value again into a new new Reader((env) => f(Fn(env)))

![](img/d73681d801b4b826e0b2a293897bbba4_130_0.png)

## 4.9 LINQ Native Query syntax: Functor Support

Did you know that if you implement a Select method in any type you can use the from ... in ... select Linq syntax???

Here I will rename the Map() method of our Id<T> to Select()

```
public class Id<T>
{
    public T Value { get; set; }
```
