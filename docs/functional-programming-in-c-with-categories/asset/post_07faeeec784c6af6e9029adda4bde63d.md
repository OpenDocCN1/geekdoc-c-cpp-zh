
## Monoid Homomorphism

Category Theory

Monoid Homomorphism is a thing of beauty and a profound concept, that can be found everywhere in mathematics, logic, and programming. It captures the idea of Preserving the Structure when we map something from one monoid structure to another. The word homomorphism comes from the ancient Greek language: ὁμός (homos) meaning "same" and μορφή (morphe) meaning "form" or "shape".

A monoid homomorphism between two monoids (⊗, M) and (⊙, N), is a function :

φ: M → N

Such that:

φ(a₁ ⊗ a₂)=φ(a₁) ⊙ φ(a₂)

φ(1ₘ)=1ₙ

where 1ₘ and 1ₙ are the identities of N and M aka our monoid empties.

![](img/d73681d801b4b826e0b2a293897bbba4_68_0.png)

This means that if we map the a₁ ,a₂ and a₁ ⊗ a₂ to the φ(a₁), φ(a₂) and φ(a₁ ⊗ a₂) then the φ(a₁) ⊙ φ(a₂) multiplication with the second monoid ⊙ should be exactly equal to φ(a₁ ⊗ a₂). The structure should be preserved.

Also the φ maps the identity element of the M monoid 1ₘ to the identity element of the N monoid.

![](img/d73681d801b4b826e0b2a293897bbba4_68_1.png)

Let us see another example:

```
("monoid" + "homomorphism ").Length == ("monoid".Length + "homomorphism ".Length);
```

Or this one:

```
var totalSum = array => array.Aggregate( 0 , (a, b) => a + b)
```

```
totalSum([1, 2, 3, 4].concat([7, 8])) === totalSum([1, 2, 3, 4]) + totalSum([7, 8])
```

where the totalSum function is a Homomorphism over the Sum monoid (θ, (x, y) => x + y) and the Array Monoids. The point of all this is that we can parallelize over the list by splitting it to smaller chunks and process them independently. This is the idea behind the famous pattern called mapReduce

if we have a big list, we can slice it and apply a function to each chunk, then fold each slice and then fold the results of the chunks.

```
var biglist = Enumerable.Range(1, 1000000);
```

```
Func<IEnumerable<int>, Func<int, IEnumerable<IEnumerable<int>>>> slice = list => size =>
{
  var accumulation = new List<IEnumerable<int>>();
  for (int i = 0; i < list.Count(); i += size)
    accumulation.Add(list.Skip(i).Take(size));
  return accumulation;
};
```

```
var mapReduce = list => monoid => map =>
list.Select(chunk =>
  chunk.Select(Convert.ToDecimal).Select(map).Aggregate(monoid.Empty, monoid.Concat)
).Aggregate(monoid.Empty, monoid.Concat);
```

```
var chunks = slice(bigList)(10000);
var sum = mapReduce(chunks)(new SumDecimal())(x => x + 1);
```

Of course C# already has embedded a degree of parallelism in TPL(Task Parallel Library) and the PLINQ extension of LINQ. The point of this section is why monoids are related with parallelism.

The theoretical support of the map reduce pattern came from the work of Richard Bird and Lambert Meertens that come up with the Bird-Meertens formalism and the Homomorphism lemma specifically for lists that say that a function h on lists is a list homomorphism :

```
h([])=e
h(a.concat(b))=h(a) • h(b)
```

if only if there exist a function f and an operation • - so the following hold

```
h = reduce(•) • map(f)
```

reduce (•) here means the operation (e1•(e2•(e3 • e4))) folding the elements on a list. If there is a Homomorphism it should be able to be decomposed in a map followed by a reduce.

A Homomorphism in a list means Parallelism. Let’s see another example.

Counting words in a large document is also something that can be done in parallel.

- 1. We can split the document in chunks and
- 2. then count the words in each chunk and add them in a dictionary.
- 3. Then we can merge the dictionaries because they form a monoid

Here the monoid is the dictionary as a Dictionary. We can prove that if we have a IDictionary<TKey, TValue> with keys of type TKey and values of type TValue and TValue is a monoid then we can create a IDictionary monoid:

```
var dictionary1 = new Dictionary<string, int> {
  { "or", 2 },
  { "and", 3 },
  { "the", 4 }
};

var dictionary2 = new Dictionary<string, int> {
  { "or", 1 },
  { "and", 5 },
  { "jim", 1 },
  { "his", 1 }
};
```

```
var merged = new DictionaryMonoid<string, int>(new Sum()).Concat(dictionary1, dictionary2);
```

```
public class DictionaryMonoid<TKey, TValue> : IMonoid<IDictionary<TKey, TValue>>
{
	private IMonoid<TValue> ValueMonoid { get; }
	public DictionaryMonoid(IMonoid<TValue> monoid) => ValueMonoid = monoid;
	public IDictionary<TKey, TValue> Empty => new Dictionary<TKey, TValue>();
}

public IDictionary<TKey, TValue> Concat(IDictionary<TKey, TValue> x, IDictionary<TKey, TValue> y)
{
	var merge = y.ToDictionary(entry => entry.Key, entry => entry.Value);
	foreach (var keyValue in x)
		if (merge.ContainsKey(keyValue.Key))
			merge[keyValue.Key] = ValueMonoid.Concat(merge[keyValue.Key], keyValue.Value);
		else
			merge[keyValue.Key] = keyValue.Value;
	return merge;
}
```

```
}
}
public class Sum : IMonoid<int>
{
    public int Concat(int x, int y) => x + y;
    public int Empty => 0;
}
```

Run This: Fiddle

this idea means that we **can parallelize the word counting problem, just because we were able to recognize a monoid.**

This page intentionally left blank.

## 3 Algebraic Data Types

> “Lists come up often when discussing monoids,
> and this is no accident: lists are the “most fundamental” Monoid instance.”
> Monoids: Theme and Variations (Functional Pearl)

Many of the most popular data structures like a list have definitions like this:

> “A list is **either** an **empty list** or a **concatenation** of an **element** and a **list.**”

In the above sentence if we replace the word element with a, the either with +, and the concatenation with * we get the algebraic definition of a list:

**List (a)** = [ ] + **a** * **List(a)**

This definition is recursive because the term List appears on both sides of the definition. In C#, this translates to something like the following:

```
public abstract class ListBase<T> { }

public class Cons<T> : ListBase<T> {
    public ListBase<T> Rest { get; set; }
    public T Value { get; set; }

    public Cons(T value, ListBase<T> rest)
    {
        this.Value = value;
        this.Rest = rest;
    }
}

public class Empty<T> : ListBase<T> { }
```

![](img/d73681d801b4b826e0b2a293897bbba4_73_0.png)

```
var list = new Cons<int>(value: 2,
    rest: new Cons<int>(value: 5,
        rest: new Empty<int>()));
```

This definition is the base definition of a List. Furthermore, because of its significance, we will often use this simple algebraic form of the List to display many functional ideas.

In practical terms giving recursive definitions means that we can progressively compose more complex entities out of simpler objects by applying some operations between them. The following three ways to combine structures are the most pervasive in programming.

- 1. **Product** [object-oriented equivalent: **composition**]: In our definition of the list the object literal that has two properties is a product
  `Cons(T value, ListBase<T> rest)`
- 2. **Coproduct** [object-oriented equivalent: **inheritance**]: In our definition of the list, `Cons<T> : ListBase<T>`, and `Empty<T> : ListBase<T>` form a co-product, commonly called a union type. In object-oriented terms, simple inheritance is a union type.
- 3. **Recursive Type** [object-oriented equivalent: **a type that contains objects of the same Type or inheriting type**]: The fact that in
  `Cons<T> : ListBase<T> {public ListBase<T> Rest { get; set; }}`
  the Rest is a ListBase<T>Type means that we have a recursive definition.

The fact that a data type can be formed by applying some operations between them gives them the name **algebraic**. An **algebraic data type** is a kind of composite type.

Now, if we define those three operations in any language or programming paradigm, we can define a list by following the algebraic definition “A list is **either** an **empty list** or a **concatenation** of an **element** and a **list.**”. If someone tells us how to form a product a coproduct and a recursive type in Java or python or Elm we can instantly write a definition of a list without the need to be experts of the language.
