```
let newList =
list
  | Seq.skip(fun x -> x<n)
  | Seq.skip 1
  | Seq.toList
let newElementName = elementNeeded - 1
for 1 in getCombinationFunction newList newElementName (currentList@[])
```

```
do

  yield 1 ]
```

```
getCombination list elementNeeded []
```

```
getCombination [1; 2; 3; 4] 3
```

# Execution result

```
val getCombination :list list -> elementNeeded:int -> int list list
val it : int list list = [[1; 2; 3]; [1; 2; 4]; [1; 3; 4]; [2; 3; 4]]
```

The keyboard The telephone keyboard enables you to input non-numeric characters as well as number characters. Listing 7-47 demonstrates how to get the character sequence from number inputs.

# LISTING 7-47 Generating output from digital-character input

```
let letters =
[
  '0', ['O']
  '1', ['I']
  '2', ['Z'; 'A'; 'B'; 'C']
  '3', ['O'; 'E'; 'F']
  '4', ['A'; 'G'; 'H'; 'I']
  '5', ['S'; 'J'; 'K'; 'L']
  '6', ['M'; 'N'; 'O']
  '7', ['T'; 'P'; 'O'; 'R'; 'S']
  '8', ['B'; 'T'; 'U'; 'V']
  '9', ['9'; 'W'; 'X'; 'Y'; 'Z']
]
|> Map.OfList
```

```
let mutable currentState = ('0', -1)
let mutable result = System.Collections.Generic.List<>()
```

```
let output() =
  let char, times = currentState
  if times >=0 then
    let l = letters.[char]
    let len = 1.Length
```