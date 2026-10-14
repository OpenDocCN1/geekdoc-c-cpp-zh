```
```haskell
bimap (g1 <<< f1) (g2 <<< f2) (Tuple x y)
    = bimap g1 g2 <<< bimap f1 f2 (Tuple x y) — Given
Tuple (g1 <<< f1 $ x) (g2 <<< f2 $ y)
    = bimap g1 g2 <<< bimap f1 f2 (Tuple x y) — Subst into ❶
Tuple (g1 (f1 x)) (g2 (f2 y))
    = bimap g1 g2 <<< bimap f1 f2 (Tuple x y) — Compose equivalence
Tuple (g1 (f1 x)) (g2 (f2 y))
    = bimap g1 g2 (bimap f1 f2 (Tuple x y)) — Compose equivalence
Tuple (g1 (f1 x)) (g2 (f2 y))
    = bimap g1 g2 (Tuple (f1 x) (f2 y)) — Subst into ❶
Tuple (g1 (f1 x)) (g2 (f2 y))
    = Tuple (g1 (f1 x)) (g2 (f2 y)) — Subst into ❶
```
```