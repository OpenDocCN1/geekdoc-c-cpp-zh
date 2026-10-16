
```
public async Task<string> GetNameByIdAsync(int clientId)
    => await clients.GetByIdAsync(clientId)
        .Map(client => client.Name).Case_switch
{
    LeftCase<string, string>(var error) => error,
    RightCase<string, string>(var name) => name,
    _ => throw new NotImplementedException(),
};
}
```

Note :The use of .Case without the need to first await

Github: source

## 4.17 Functors from Algebraic Data Types

We have seen an implementation of the map function for our algebraic definition of the list data structure in section 3.4. I will restate the implementation here:

```
public class Cons<T> : ListBase<T>
{
    ...
    public override ListBase<T1> Map<T1>(Func<T, T1> f) =>
        new Cons<T1>(f(Value), Rest.Map(f));
}
```

```
public class Empty<T> : ListBase<T>
{
    public override ListBase<T1> Map<T1>(Func<T, T1> f) => new Empty<T1>();
}
```

Now that we know much more about functors, we can extrapolate the implementation of the map for a binary tree. So, let us go from Linear to quadratic.

The tree is also a recursive data structure. The definition of a binary tree is this:

Tree (a)= leaf(a) + Node(Tree(a), Tree (a))

Which states that a Tree(a) can be a Leaf (a) or a Node of two Trees of type a.

[Sidenote: The list can be viewed as a tree, which has its Right side of all nodes are always leaves: Tree a = Leaf a + Node (Leaf a) * (Tree a) ≅ List a = a + a * (List a) ]

```
public abstract class Tree<T>
{
    public abstract Tree<T1> Map<T1>(Func<T, T1> f);
}
```

```
public class Node<T> : Tree<T>
{
    public Tree<T> Left { get; set; }
    public T Value { get; set; }
    public Tree<T> Right { get; set; }

    public Node(Tree<T> left, Tree<T> right)
    {
        this.Left = left;
        this.Right = right;
    }
}
```

```
public class Leaf<T> : Tree<T>
{
    public T V { get; }
    public Leaf(T v) => V = v;
}
```

In order to create a functor based on this algebraic data type we define a valid **map** method. We will again follow our **method of structural induction** in order to define the **map**.

First, because it is a **coproduct**, we must define the map method in both subtypes :Leaf and Node of the coproduct.

- 1. We start with the Leaf which is the base case of the structural induction. We must return something of the same type. That’s why we return a new Leaf with the function applied to the value
   
  `Tree<T1> Map<T1>(Func<T, T1> f) => new Leaf<T1>(f(V))`

**A leaf is just an Identity functor.** Hopefully, you recognized it.

- 2. The Node part is a product of two trees (Left, Right) both are of the same type as the one for which we want to define the map. The only way to deal with it is to assume that both must have a map function already in place that works as expected (this is the inductive hypothesis again),
  
  `Tree<T1> Map<T1>(Func<T, T1> f) => new Node<T1>(Left.Map(f), Right.Map(f))`

```
this.Left = left;
Value = value;
this.Right = right;
}
```

Tree (a)= leaf(a) + Node(Tree(a), a, Tree (a))

Can you extend the previous definition of map to also lift the value of the node?

Can you write a symbolic equation for the definition of the map for this tree version?

## C# 8.0 Pattern Matching

We can rewrite the map using the switch and extension methods in this way we skip the custom MatchWith method

```
public static Tree<T1> Map<T, T1>(this Tree<T> @this, Func<T, T1> f) =>
    @this switch
    {
        Leaf<T> { Value: var v } => new Leaf<T1>(f(v)),
        Node<T> { Left: var l, Right: var r } =>
            new Node<T1>(l.Map(f), r.Map(f)),
    };
```

Run This: .Net Fiddle

## 4.18 Applicative Functors

Applicative is a relatively easy concept to grasp. It is a functor F that contains a function ( a→ b ) instead of just a value, and we must provide a valid method that can take another functor with a value F(a) and give an F(b). We call this apply (usually the method is named Ap):

Ap: F(a → b) → F(a) → F(b)

![](img/d73681d801b4b826e0b2a293897bbba4_160_0.png)

you can compare this with the map signature Map : (a → b) → F(a) → F(b) the only difference is the initial F.

If we take the Identity functor as an example, we can implement the apply as follows:

## 4.19 Reader Applicative Functor optional

A reader applicative is a reader that has a function stored as the expression expr. The implementation is a bit complex. Try to imagine that you want to combine a reader that has a function and a reader that has just a value. This is my implementation:

```
public static class FunctionalExtensions
{
    public static Reader<Env, T1> App<Env, T, T1>
        (this Reader<Env, Func<T, T1>> @this, Reader<Env, T> fa) =>
    new Reader<Env, T1>(env => { return @this.Map(f => fa.Map(f).Run(env)).Run(env); });
}
```

```
var r = new Reader<(int, int), Func<int, int>>((g => (r) => g.Item1 + r))
    .App(new Reader<(int, int), int>(g => 1))
    .Run((1, 2));
```

if we take the applicative operation

Ap: f(a→b)→f(a)→f(b) (this is the name for ⟨⊗...⟩)

for the reader specifically by substituting the f with the ((→) env) [that’s (env →_)] we get

⟨⊗⟩: ((→)env) (a→b) → ((→)env) a → ((→)env) b

With some reductions we get the form

(env → (a→b)) → (env → a) → (env → b)

If for example, we have a curried function of arity 2 like x=>y=>y+x we can do that

⟨add ⊗ 1 ⊗ 2⟩ → ⟨1+2⟩ we will get a reader of the addition

```
var t = new Reader<object, Func<int, Func<int, int>>>((g => x1 => y1 => x1 + y1))
    .App(new Reader<object, int>(g => 1)).App(new Reader<object, int>(g => 1))
    .Run(default);
```

Category Theory Monoidal Functor

Let (C,⊗_C,1_C) and (D,⊗_D,1_D) be two monoidal categories. A lax monoidal functor between them is

- 1. a functor F:C→D.
- 2. a morphism ε:1_D→F(1_C)

3. a natural transformation μ_{x,y}:F(x)⊗_D F(y)→F(x⊗_C y) for all x,y∈ C

ε:1_D→F(1_C) represents the pure operation of the applicative, that allows us to get into an applicative

F(x)⊗_D F(y)→F(x⊗_C y) is the applicative operation of ap. The interesting thing with this definition is that it connects the “multiplication” ⊗_D of one category with “multiplication” ⊗_C of the other category.

In our example above the equivalence is that the multiplication ⊗_Int : (+) of the integers is now the same as the ⊗_Reader, applicative operation ap ⟨ ⟩ of the reader :

(+) → is the same ⟨ ⟩

```
Reader(g=>x=>y=>y+x).ap(Reader(g => 1)).ap(Reader(g => 2)).run({});
```

Two completely different domains but actually. ap is equivalent with + in a different level of abstraction. Cool right.

Also as we will see in the traversable section the Arrays “multiplication” ⊗_Array concat (:) will be lifted to the now the same as the ⊗_Reader, applicative operation ap ⟨ ⟩ of the reader

(:) → ⟨ ⟩

```
Reader(g=>x=>y=>[y].concat(x)).ap(...).ap(Reader(...)) ;
```

(Hopefully you would recognized that μ_{x,y}:F(x)⊗_D F(y)→F(x⊗_C y) is a monoid homomorphism)

```
public Id<T1> Bind<T1>(Func<T, Id<T1>> f) => f(Value);
```

The new thing here is the bind method. Id<T1> Bind<T1>(Func<T, Id<T1>> f) => f(Value)

```
Id(5).Bind(x=>Id(x+1)) == Id(6)
```

this bind method has a type of Bind:(T→ M <T1>) →M<T1> that takes a function T→M <T1>, which, when provided with the contained value v it returns a new monad M<T1> of type T1.

```
var result = new Id<int>(2)
    .Bind(x => new Id<int>(2)
        .Bind(y => new Id<int>(x + y)));
```

Let’s put a monad in a monad and Bind with the identity x=>x to get the initial Monad back.

```
var IdInId = new Id<int>(5).Map(x => new Id<int>(x + 1));
var justId = IdInId.Bind(x => x);
```

The difference between bind and map in the identity monad is that map passes the lifted value to a monad constructor Id(f(v)) while bind does not: f(v). In other monads the map will be significantly different than the bind.

The same reasoning goes for all functors, here some other examples leading to the same situation of a Functor in a Functor if we use the Map:

```
New IO(()=>5).Map(x=> new IO(()=> x+1)) === new IO(()=>new IO(()=> 6))
```

```
var a = new[] { 4 }.Select(x => new[] { x + 1 });
var b = new[] { new[] { 4 } };
```

```
new Some<int>(4).Map(x=> new Some<int>(x+1)) === new Some (new Some (5))
```

so its usual to define a Bind in most Functos and thus upgrade them into monads.

## Conventions: Bind and SelectMany

As a convention we will name our mapping method Bind nonetheless in some instances we might also use SelectMany if we need LINQ support. Map and Select will be used interchangeably in this book. The language-ext library provides Bind and SelectMany methods aliases
