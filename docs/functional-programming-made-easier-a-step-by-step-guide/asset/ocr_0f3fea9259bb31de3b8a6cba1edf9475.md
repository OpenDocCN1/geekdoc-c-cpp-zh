that map back to the SAME Category are known as *EndoFunctors*. So all *Functors* in PureScript are really EndoFunctors but everyone just says *Functors*.

There’s another really important requirement of Functors.

> Functors preserve Categorical Structure. In Abstract Algebra, functions that preserves the Algebraic Structure of say a Group are called *Homomorphism* (*Homo* means *same* and *morph* means *shape*). Here Functors are like Homomorphisms since they too preserve the Categorical Structure.

If a Object a has a Morphism to Object b then a Functor must preserve that same Morphism between the Objects when mapping them into the new Category. It also, cannot drop any Objects or Morphisms when mapping nor can it create any new Objects or Morphisms that weren’t in the original Category:

![](bbox=[0.068, 0.328, 0.942, 0.688])

Here the Functor F maps both Objects and Morphisms from Category C to D.

In this diagram, F maps a to F a and b to F b, i.e. maps all Objects (not all mappings shown).

It also shows that F maps f to F f, i.e. maps all Morphisms (not all mappings shown).

When we look at map in PureScript with the implied Parentheses: