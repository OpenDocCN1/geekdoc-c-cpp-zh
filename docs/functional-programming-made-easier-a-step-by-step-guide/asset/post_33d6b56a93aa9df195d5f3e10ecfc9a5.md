
specific Types. `m` is the effect Monad that’s used during the Evaluation. Your component is **Evaluated** each time an event occurs that warrants running your component code.

④ `H.mkComponent` makes a Component. It takes some Parameters, which are currently missing.

Let’s look at `H.mkComponent` in detail:

```
mkComponent
  :: ∀ state query action slots input output m
   • ComponentSpec state query action slots input output m
  -> Component query input output m
```

This may seem intimidating at first glance, but these Type Parameters are used over and over again throughout Halogen, so you’ll get quite familiar with them soon enough.

Here are their definitions:

+   - `state` - This is the Type that is your State. Components maintain their own internal State.
+   - `action` - This is the Type for Actions that your Component can take. In our `Counter` Component, we will have the Actions, `Increment` and `Decrement`, which will be triggered by the user clicking on the appropriate buttons.
+   - `slots` - This is the Row Type that defines your Children. When your Component has no Child Components, you can simply just make this an Empty Row, i.e. `()`.
+   - `input` - This is the Type for the Input you’ll get from your Parent Component or from the Application if you’re a Top-level Component.
+   - `output` - This is the Type for the messages you send back to your Parent or the Application if you’re a Top-level Component.
+   - `query` - This is what’s called the **Query Algebra**, i.e. operations you can perform on your Component. If you’ve programmed in Object Oriented Languages you can think of this as the Public Interface to your Component.

Now let’s look at `ComponentSpec` in detail:

```
import Halogen.HTML.Core as HC

type ComponentSpec state query action slots input output m =
  { initialState :: input -> state
  , render
      :: state
    -> HC.HTML (ComponentSlot slots m action) action
  , eval
      :: HalogenQ query action input
    ~> HalogenM state action slots output m
  }
```

+   - **initialState** - This Function gets a single Parameter of the `input` Type and will initialize the `state`.
+   - **render** - This Function creates the Virtual DOM, using Functions like `HH.div`, `HH.input`, `HH.text`, etc. It takes a single Parameter of the `state` Type and uses this data to render the Virtual DOM Elements.
+   - **eval** - This is a Function that Evaluates your Component. We don’t ever write this Function, but instead use a helper called `mkEval` where we pass an `EvalSpec`.

Let’s add the ComponentSpec to our code:

```
component
  :: ∀ m
    . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: ??? ①
  , render ②
  , eval: H.mkEval ??? ③
  }
```

① We haven’t defined Input or State yet, so we cannot code this just yet.

② render it typically a fairly large Function and is usually in the same module as the component code.

③ H.mkEval wants an EvalSpec, but we don’t know anything about EvalSpec yet.

Since we’re writing a simple Counter Component, let’s define the following:

```
type Input = Int
type Output = Int
type State = { count :: Int }
```

Parent’s render Function no longer renders you or, if you’re a Top-level Component, when the Application explicitly calls dispose on you.

There is a default EvalSpec:

```
defaultEval
  :: ∀ state query action slots input output m
    . EvalSpec state query action slots input output m
defaultEval =
  { handleAction: const (pure unit)
  , handleQuery: const (pure Nothing)
  , receive: const Nothing
  , initialize: Nothing
  , finalize: Nothing
  }
```

All of the defaults do nothing. So, this makes overriding easy. Let’s use the default and just override initialize and finalize:

```
import Data.Maybe (Maybe(..)) ①

data Action ②
  = Initialize
  | Finalize

component
  :: ∀ m
    . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \i -> { count: i }
  , render
  , eval: H.mkEval H.defaultEval {
      initialize = Just Initialize ③
    , finalize = Just Finalize ④
    }
  }
  where
  ???
```

① Import Maybe and its Data Constructors.

② Define 2 Actions to handle the initialization and finalization of our Component.

③ We’re overriding initialize from defaultEval to be the Initialize Action. Since this is optional, it’s a Maybe.

④ We’re overriding finalize from defaultEval to be the Finalize Action.

Notice the where keyword at the bottom of the above code block. I like to put all of my Component Functions, e.g. render, handleAction, etc. under a where.

You don’t have to do this, but if you pass any Parameters to the component Function when you construct your Component, those Parameters will be in scope in every Function under the where.

I’ve found that I rely on this more than not, which is why I always code my components this way.

Now, let’s write a stub for the render Function:

```
-- ABOVE CODE REDACTED
where
render :: State -> H.ComponentHTML Action Slots m
render _ = HH.text "Stubbed out" ①
```

① A single Text Node.

All we need now is to add Type Aliases for Query and Slots:

```
type Query = Void ①

type Slots :: ∀ k. Row k ②
type Slots = () ③
```

① For now, there are no Queries. So we use Void.

② Since we’re specifying an empty Row, the compiler will complain that The inferred kind for the type declaration Slots contains polymorphic kinds. And it will suggest you add a Type Signature since this definition is a top-level one. Remember, polymorphic kinds means that we can specify any Kind. Some examples of Kinds are Type, Constraint, Symbol, and Row. Since the Row is empty, it could be anything.

③ For now, there are no Child Components.

We have a compiler error on the Type Signature of component:

```
component
  :: ∀ m
  . MonadAff m
  -- COMPILER ERROR!!
  => H.Component Query Input Output m
```

Here’s the error:

![](img/8c0e9b687c62642e828ccb5481e11313_1584_0.png)

Looks like Query takes a Parameter, so let’s give it one:

```
type Query a = Void -- COMPILER ERROR!!
```

Now, we have a different error:

![](img/8c0e9b687c62642e828ccb5481e11313_1584_1.png)

Looks like we cannot have a Phantom on Type Aliases. We can change it to a real Type or we can use a Type called Const:

```
newtype Const a b = Const a
```

This lets us do:

```
import Data.Const (Const)

type Query :: ∀ k. k -> Type ①
type Query = Const Void
```

① Const takes 2 parameter. We are only Partially Applying Void to Const. Because of this, the compiler

doesn't know what Kind the second Parameter is, which is why we need this Type Signature. It basically says, we take any Kind, k, and return a Type.

We could've made Query a real Type, which wouldn't require the use or import of Const:

```
newtype Query :: ∀ k. k -> Type ①
newtype Query a = Query Void
```

① The Type Signature is unchanged and still required since a is unknown and a Phantom Parameter.

The choice is yours. Pick your poison. I'm going to choose the use of Const.

Now, you should have a single compiler WARNING since we're not using Halogen.HTML.CSS yet:

```
module Component.Counter where

import Prelude

import Data.Const (Const)
import Data.Maybe (Maybe(..))
import Effect.Aff.Class (class MonadAff)
import Halogen as H
import Halogen.HTML as HH
import Halogen.HTML.CSS as HC -- COMPILER WARNING!!

type Input = Int
type Output = Int
type State = { count :: Int }

type Slots :: ∀ k. Row k
type Slots = ()

type Query :: ∀ k. k -> Type
type Query = Const Void

data Action
  = Initialize
  | Finalize

component
  :: ∀ m
  . MonadAff m
  => H.Component Query Input Output m
component = H.mkComponent
  { initialState: \i -> { count: i }
  , render
  , eval: H.mkEval H.defaultEval {
      initialize = Just Initialize
    , finalize = Just Finalize
    }
  }
where
render :: State -> H.ComponentHTML Action Slots m
render _ = HH.text "Stubbed out"
```

Now that this compiles, we should add a handleAction Function so we can log when the Component is initialized and finalized:
