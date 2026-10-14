```
takeWhile :: ∀ a. (a -> Boolean) -> List a -> List a
takeWhile _ Nil = Nil ①
takeWhile pred (x : xs) = ②
  if pred x then x : takeWhile pred xs else Nil
```

We’re going to use Mathematical Substitution as we’ve done before. We can do this thanks to Referential Transparency:

```
-- starting with
takeWhile (_ <= 2) (1 : 2 : 3 : Nil)
-- substituting into ②
if (_ <= 2) 1 then 1 : takeWhile (_ <= 2) (2 : 3 : Nil) else Nil
-- evaluating we get
1 : takeWhile (_ <= 2) (2 : 3 : Nil)
-- substituting into ②
1 : (if (_ <= 2) 2 then 2 : takeWhile (_ <= 2) (3 : Nil) else Nil)
-- evaluating we get
1 : (2 : takeWhile (_ <= 2) (3 : Nil))
-- substituting into ②
1 : (2 : (if (_ <= 2) 3 then 3 : takeWhile (_ <= 2) Nil else Nil))
-- evaluating we get
1 : (2 : takeWhile (_ <= 2) Nil else Nil)
-- substituting into ①
1 : (2 : Nil)
-- removing Parentheses
1 : 2 : Nil
```

# 5.37. Writing dropWhile

dropWhile is to takeWhile what drop is to take.

Add this to your tests:

```
log $ show $ dropWhile (_ > 3) (5 : 4 : 3 : 99 : 101 : Nil) ①
log $ show $ dropWhile (_ == -17) (1 : 2 : 3 : Nil) ②
```

① Prints (3 : 99 : 101 : Nil)

② Prints (1 : 2 : 3 : Nil)

Consult Pursuit for the details and write dropWhile before moving on.