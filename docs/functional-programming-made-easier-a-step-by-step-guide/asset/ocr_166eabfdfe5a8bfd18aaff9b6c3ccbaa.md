```
data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild Int ①
  | RaiseParent
```

① This Int is the count Value NOT which Child.

We’ll need to add another Parameter to FromChild that contains the slot Value.

Go ahead and change the FromChild Data Constructor to have another Parameter for slot, then change handleAction code to set the Child’s count Value to 123 in FromChild keeping the existing log functionality and finally update the render Function where FromChild is used to map Child Outputs to Actions to include the Child’s slot identifier, i.e. it’s slot number.

Then return here.

First, we’ll add another Int to FromChild.

```
data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild Int Int ①
  | RaiseParent
```

① The first Int is the slot number since we’re going to Partially Apply this in the render Function.

Those 2 Int Parameters to FromChild are confusing. Which Int is which again? Let’s fix that:

```
type SlotNum = Int ①
type CounterValue = Int

data Action
  = Initialize
  | Finalize
  | Increment
  | Decrement
  | FromChild SlotNum CounterValue ②
  | RaiseParent
```