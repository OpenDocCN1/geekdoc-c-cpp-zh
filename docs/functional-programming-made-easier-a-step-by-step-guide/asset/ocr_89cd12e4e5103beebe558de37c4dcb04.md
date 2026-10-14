# 18.1.1. Composing Side-effect Functions

Now that we have a working Function, we should step back and ask ourselves can we make this better?

It’s not obvious how we can. And that’s too bad because the Pure version, h', was so simple:

```
h' = g' <<< f'
```

It’s clear that h' is superior to h. The code for h is painful to write and the process is error-prone due to its complexities. With h', we can just inline the solution, but with h, we’re forced to write a Function to compose f and g.

This is hardly ideal. Maybe we can write some library Functions that will make things better.

Let’s try that by writing a compose Function that will let us compose Side-effect Functions. How might we do that?

That’s a hard question to answer in one step. Instead, let’s attempt something a bit more attainable. We’ll write a Function that lets us compose Functions that return, as their Side-effect, a String stating that they were called and what they did.

Let’s call it composeDebuggable since it’ll compose any Function that returns debugging information:

```
composeDebuggable :: ???
```

Writing the Type Signature here isn’t obvious. Let’s look at the Type Signature for the regular compose Function to see if we can gain any insight. Looking to Pursuit we find:

```
class Semigroupoid a where
  compose :: ∀ b c d. a c d -> a b c -> a b d

infixr 9 compose as <<<
```

Wow. That’s not confusing at all. Okay, so first, what’s a Semigroupoid?

A Semigroupoid is a Category minus the identity morphism requirement.

Remember, a Category consists of Objects and Morphisms. Each Object has an Identity Morphism (this part is NOT part of a Semigroupoid). And Morphisms are composable (this part IS part of a Semigroupoid).

We can generalize Semigroupoids as composable things. And if that’s true, then we can make Function an instance of Semigroupoid since Functions can be composed: