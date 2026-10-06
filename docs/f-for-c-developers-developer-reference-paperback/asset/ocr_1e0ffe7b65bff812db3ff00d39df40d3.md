```
let dutchFlag(list: array, (low, high)) =
  let swap(i,j) =
  let temp <- list[i]
  list[i] <- list[j]
  list[j] <- temp

  let mutable i = 0
  let mutable lowPointer = 0
  let mutable highPointer = list.Length - 1

  while i <= highPointer do
    let value = low, list[i], high
    match compare value with
      | Lower ->
        swap(lowPointer, i)
        lowPointer <- lowPointer + 1
        i <- i + 1
      | Higher ->
        swap(highPointer, i)
        highPointer <- highPointer - 1
      | Middle ->
        i <- i + 1
```

let arr = [1; 9; 8; 2; 4; 3; 6; 7; 5; 0]
dutchFlag(arr, 3, 7)

**Finding the longest increasing sequence** To determine the longest increasing sequence (LIS), use an array variable (named DP) to hold the current LIS up to the current index. For example, if the value in DP.[10] is 3, the LIS for array.[0..9]. Value of DP.[i] is updated only when the new value (DP.[j] + 1) is higher than the current value (DP.[i] < DP.[j] + 1) and the value is still increasing (array.[i] > array.[j]). Seeing List 7-17.

**LISTING 7-17** Longest increasing sequence code

```
let list = [10; 22; 9; 31; 50; 41; 60; 80]
let DP = Array.create list.Length 1
nlet findMax() =
  let mutable maxLength = 1
  for i = 1 to list.Length - 1 do
    for j = i - 1 downto 0 do
      if list[i] > list[j] &&
        DP[i] < DP[j] + 1 then
          DP[i] <- DP[j] + 1

  maxLength <- max maxLength DP[i]

findMax()
```

* Asterisk*