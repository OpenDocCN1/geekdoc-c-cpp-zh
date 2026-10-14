
However, it’s the idea that Functions are no different from Integers where the real power is. In our earlier append example, we struggled to pass a Predicate Function because the language simply had no mechanism.

Now that Java pilfered this feature from Functional Languages, we can write:

```
import java.util.function.Function;

public class HelloWorld {

    public static Function<String, Boolean> isSmall =
        s -> s.length() < 10; ①
    public static Function<String, Boolean> isOddLength =
        s -> s.length() % 2 != 0; ①
    public static Boolean isSmall(String s) {
        return s.length() < 10;
    }
    public static String appendIf(Function<String, Boolean> pred,
                    String s, String append) {
        if (pred.apply(s)) ②
            return s + append;
        else
            return s;
    }
    public static void main(String[] args) {
        System.out.println(appendIf(isSmall, "Hello World", "!!!"));
        System.out.println(appendIf(isOddLength, "Hello World", "!!!"));
    }
}
```

① These special types of Functions in Java can be passed to appendIf just like we passed the Strings, s, and append.

② We apply the Parameter, s, to our Predicate Function, pred.

I wish I had this facility back in the early days of Java but this kind of thing is commonplace in Functional Languages.

Let’s look at the PureScript equivalent:

```
```purescript
module Main where

import Prelude

import Data.String.CodePoints (length)
import Effect (Effect)
import Effect.Console (log)

isSmall :: String -> Boolean
isSmall s = length s < 10

isOddLength :: String -> Boolean
isOddLength s = length s `mod` 2 /= 0

appendIf :: (String -> Boolean) -> String -> String -> String
appendIf pred s append = if pred s then s <> append else s

main :: Effect Unit
main = do
  log $ appendIf isSmall "Hello World" "!!!"
  log $ appendIf isOddLength "Hello World" "!!!"
```
```

❶ These Functions are just run-of-the-mill Functions. No special syntax needed.

I don’t expect you to understand this code just yet but I wanted to show you the terseness of PureScript compared with Java. Granted, if you’re a Java programmer, the PureScript version will feel very foreign at first.

Regardless, there’s a beautiful lack of parentheses, commas, semi-colons, curly-brackets and accessor types, i.e. `public` and `static`. While this may be jarring at this point, I promise that you will get spoiled by this very quickly.

Where Java uses `Function<String, Boolean>`, PureScript uses `String -> Boolean`.

In Java, there is a special protocol to use a Function that’s been passed as a Parameter, `pred.apply(f)`. In PureScript, it’s no different than calling any other Function, `pred f`.

Just for fun, let’s look at the same code in Haskell:

```
const isEven = n => n % 2 === 0;
const upperLower = n => {
  if (isEven(n)) return String.prototype.toUpperCase;
  else return String.prototype.toLowerCase;
};

console.log(upperLower(0).apply("this should be output in uppercase"));
console.log(upperLower(1).apply("THIS SHOULD BE OUTPUT IN LOWERCASE"));
```

① If n is even then we return a Function to convert strings to uppercase. Otherwise, we return a Function to convert strings to lowercase.

Let’s see how we’d write this in PureScript:

```
module Main where

import Prelude

import Data.String.Common (toLower, toUpper)
import Effect (Effect)
import Effect.Console (log)

isEven :: Int -> Boolean
isEven n = n `mod` 2 == 0

upperLower :: Int -> (String -> String)
upperLower n = if isEven n then toUpper else toLower

main :: Effect Unit
main = do
  log $ upperLower 0 "this should be output in uppercase"
  log $ upperLower 1 "THIS SHOULD BE OUTPUT IN LOWERCASE"
```

Once again, the PureScript example will not completely make sense to you yet but we’re only concerned with how it contrasts with Javascript.

It’s also possible that you are not familiar with Javascript either and in that case, the best you can hope to discern from these two examples is that the syntax in PureScript is far less dense than in Javascript.

You may also notice that there’s a lot more overhead in PureScript because we have to import libraries. In this particular example, Javascript has all of the Functions we need already built-in. This is not always the case.

If you’ve spent any time working with Javascript, you’re well aware of how complicated adding libraries

can be especially if you're targeting the Browser but using a library originally written for Node.

Such is the life of a front-end developer these days.

## 2.3. Higher-order Functions

To summarize, Functional Languages treat Functions as Values, which means that they can be passed to other Functions as Parameters and can be returned from other Functions.

The technical term for this is *Higher-order Function*.

> A *Higher-order Function* is a Function that takes a Function as a Parameter, returns a Function or both.

In contrast, Functions that do not do this are known as *First-order Functions*.

Look back at the PureScript code and see if you can find the Higher-order Functions and the First-order Functions.

If you get stuck, try looking at the Javascript code. There are two First-order Functions and one Higher-order.

Let’s see how you did:

```
module Main where

import Prelude

import Data.String.Common (toLower, toUpper)
import Effect (Effect)
import Effect.Console (log)

isEven :: Int -> Boolean ❶
isEven n = n `mod` 2 == 0

upperLower :: Int -> (String -> String) ❷
upperLower n = if isEven n then toUpper else toLower

main :: Effect Unit ❶
main = do
  log $ upperLower 0 "this should be output in uppercase"
  log $ upperLower 1 "THIS SHOULD BE OUTPUT IN LOWERCASE"
```

❶ First-order.

❷ Higher-order.

In PureScript, the syntax `(String → String)` stands for a Function that takes a `String` and returns a `String`, and since this is the return type of `upperLower`, it means that `upperLower` is a Higher-order Function.

Don’t worry if this isn’t making much sense just yet, because we’ll delve into Type Signatures later, which will clarify all of this. We’re just dabbling in the code to help us get acclimated to PureScript.

## 2.4. Composition

Building larger things from smaller components is seen in nature, engineering, manufacturing and in programming. Building larger, more complex Functions by composing smaller, simpler ones is a very powerful technique.

In Math, we learned, and most likely forgot, that we can combine two Functions using Functional Composition:

```
f : Y → Z, g : X → Y ⇒ f ∘ g (x) = f(g(x)) : X → Z ∀x ∈ X
```

If you’re not used to reading Mathematical statements, this can be daunting. So let’s break this syntax down:

```
f : Y → Z
```

This states that `f` is a Function that maps elements from the Domain `Y` to the Codomain `Z`. Don’t forget that `Y` and `Z` are Sets, e.g. `Y` could be the set of Real Numbers, ℝ (this is the symbol Mathematicians use to denote Real Numbers).

What Mathematicians call `Domain` and `Codomain`, we programmers call `Input` and `Output` respectively.

What does `maps` mean in this context?

It means that `f` takes an element of `Y`, traditionally depicted by `y` and produces an element of `Z`, usually depicted by `z`.

The arrow syntax is very similar to the arrow syntax we’ve seen used in Haskell and PureScript when defining its Functions. For example:

```
negate :: Int -> Int
negate n = (-1) * n
```

`negate` is just like `f` above. Its Domain or Input is `Int` and its Codomain or Output is `Int`.

Let’s continue parsing:

```
g : X → Y
```

This states that g is a Function that maps elements from the Domain X to the Codomain Y.

Notice how g’s Codomain is the same as f’s Domain, i.e. the Output of g is the Input of f. This is a critical requirement if we are to glue these two Functions together.

```
f ∘ g (x) = f(g(x)) : X → Z ∀x ∈ X
```

The first portion states that f composed with g applied to x is equal to applying x to g and then applying those results to f. The ∘ symbol is the compose operator.

The remainder of this line states that the f composed with g maps elements from the Domain X to the Codomain Z for all elements x that are in X.

Functional Composition works from Right to Left.

```
f ∘ g
```

This is spoken as f COMPOSED WITH g or f AFTER g or f FOLLOWING g. The words AFTER and FOLLOWING help to remind us that composition is Right to Left.

```
f ∘ g (x)
```

This is spoken as f COMPOSED WITH g APPLIED TO x.

Now let’s attack the whole thing:

```
f : Y → Z, g : X → Y ⇒ f ∘ g (x) = f(g(x)) : X → Z ∀x ∈ X
```

This states that if f maps Y to Z and g maps X to Y then f COMPOSED WITH g applied to x is equal to x applied to g applied to f, which maps X to Z for all x that are elements of X.

That’s a mouthful when written out. You can see why Mathematicians use symbols like programmers do.

Speaking of programmers, how do we compose two small Functions into a larger one in code?

Here’s an example in PureScript:
