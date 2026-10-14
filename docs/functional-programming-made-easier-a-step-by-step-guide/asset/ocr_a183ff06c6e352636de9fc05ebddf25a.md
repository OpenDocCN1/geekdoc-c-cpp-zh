```
x :: Int
x = 100

_b :: Boolean
_b = true

data MyOtherType = MyOtherType
```

# Algebraic Data Types (ADTs)

There are 2 types of Algebraic Data Types, Product Types and Coproduct Types (also called Sum Types). The names reflect the process by which you determine how many inhabitants exist in a particular Type.

If the calculation involves a multiplication then it’s a Product Type. If it involves addition then it’s a CoProduct Type or Sum Type. In Math, the prefix co is added to mean the opposite (Domain, Codomain, Sine, Cosine, Tangent, Cotangent, etc.).

# Sum Types (Coproduct)

```
data Bool = True | False
```

In Haskell and Elm, this is how they define their boolean values. We can make our own Bool in PureScript since it won’t collide with Boolean.

Here Bool is the Data Type and True and False are the 2 Data Constructors:

```
mkTrue :: Bool ①
mkTrue = True ②

mkFalse :: Bool ①
mkFalse = False ②
```

① Bool is the Data Type.

② True and False are the Data Constructors

Bool can be either True or False but NOT both. That’s what makes it a Sum Type. Sum Types are also called Unions because a union in Set Theory is an OR operation. The union of Set A and Set B contains elements that are contained in A OR contained in B.

Understanding this should help you see why we separate the different possible Values of Bool with |, which is commonly used as the OR symbol in many languages, i.e. ||.