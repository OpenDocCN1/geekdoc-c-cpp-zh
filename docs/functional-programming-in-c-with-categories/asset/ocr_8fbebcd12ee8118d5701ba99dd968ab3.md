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