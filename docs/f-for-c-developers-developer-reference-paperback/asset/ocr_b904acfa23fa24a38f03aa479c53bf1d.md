```
| Node(v, 1, r) ->
let sumL = sum 1
let sumR = sum r
cont (v + sumL + sumR)

sum deepTree id
```

Step 2: Introduce *afterRight*, and use it as a continuation

```
module TreeModule =
let rec sum tree cont =
| match tree with
| Nil -> 0
| Node(v, 1, r) ->
let sumL = sum 1
// let sumR = sum r
let afterRight rValue =
cont (v + sumL + rValue)
sum r afterRight

sum deepTree id
```

Step 3: Introduce *afterLeft*, and use it as a continuation

```
module TreeModule =
let rec sum tree cont =
match tree with
| Nil -> 0
| Node(v, 1, r) ->
// let sumL = sum 1
let afterLeft lValue =
let afterRight rValue =
cont (v + lValue + rValue)
sum r afterRight
sum 1 afterLeft

sum deepTree id
```

> Note The *id* function is passed in as argument to the function *sum*.

Using the preceding steps, you can convert the recursive Fibonacci function to a CPS version. Both versions are shown in Listing 7-59.