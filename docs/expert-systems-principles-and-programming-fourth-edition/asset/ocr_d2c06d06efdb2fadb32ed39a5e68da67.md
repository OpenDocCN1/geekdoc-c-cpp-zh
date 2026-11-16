In order to analyze more general cases, the **predicate logic** was developed. Its simplest form is the **first order** predicate logic and is the basis of logic programming languages such as PROLOG. In this section, we will use the term _predicate logic_ to refer to first order predicate logic. Propositional logic is a subset of predicate logic.

Predicate logic is concerned with the internal structure of sentences. In particular, it is concerned with the use of special words called **quantifiers**, such as "all," "some," and "no." These words are very important because they explicitly quantify other words and make sentences more exact. All the quantifiers are concerned with "how many" and thus permit a wider scope of expression than does propositional logic.

# ## 2.14 THE UNIVERSAL QUANTIFIER

+   • A universally quantified sentence has the same truth value for all replacements in the same domain. The **universal quantifier** is represented by the symbol ∀ followed by one or more arguments for the **domain variable**. The symbol ∀ is interpreted as "for every" or "for all." For example, in the domain of numbers:

```
(∀ x) . (x + x = 2x)
```

states that for every x (where x is a number), the sentence x + x = 2x is true. If we represent this sentence by the symbol p, then it can be expressed even more briefly as:

```
(∀ x) (p)
```

As another example, let p represent the sentence "all dogs are animals," as in:

```
(∀ x) (p) ≡ (∀ x) (if x is a dog → x is an animal)
```

The opposite statement is "no dogs are animals" and is written as:

```
(∀ x) (if x is a dog → ¬x is an animal)
```

It may also be read as:

```
Every dog is not an animal
All dogs are not animals
```

As another example, "all triangles are polygons" is written as follows:

```
(∀ x) (x is a triangle → x is a polygon)
```

and is read "for all x, if x is a triangle, then x is a polygon." A shorter way of writing logic statements involving predicates is using **predicate functions** to describe the properties of the subject. The above logic statement can also be written as:

```
(∀ x) (triangle(x) → polygon(x))
```