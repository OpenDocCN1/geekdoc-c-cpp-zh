```
let seq = seq { for i = 0 to 10 do yield i }

for i=0 to 5 do
  let 1 = shuffleYateFisher seq
  1 |> Seq.iter(printf("%A "))
  printf """
```

**Note** Randomness and shuffling are complex topics. Don't use random number generation or shuffling algorithm for mission critical features (encryption, security, gaming engines) without assuring that you are of sufficient quality.

**Reservoir sampling** Reservoir sampling is related to the processing of large amounts of data. The algorithm is another random-selection algorithm. The algorithm is trying to get N elements from a large data set, which is so big that it is not possible to hold it in memory. In the sample code, I will use a sequence as the incoming data structure.

The algorithm first tries to fill the result set with resultSize. Once the elements are successfully retrieved, the rest of the elements are selected randomly based on a uniform distribution from 0 to the current index value. If the generated number is in the range of [0, resultSize], you can replace the result set's element with the new element, as shown in Listing 7-49.

# LISTING 7-49 Reservoir sampling algorithm

```
let rand = System.Random()

let {|InReservoirRange|_|} i resultSize =
  if i < resultSize then
    Some()
  else
    None

type ReservoirList<'a> = System.Collections.Generic.List<'a>
let result = resultSize

let reservoirSampling data result =
  let {|InReservoirRange|_|} i in {|InReservoirRange|_|} i resultSize
  data
    |> Seq.iter(fun index n ->
      match index with
      | InReservoirRange->
          result.Add(n)
      | _ ->
          let newIndex = rand.Next(index)
          match newIndex with
          | InReservoirRange ->
              result.[newIndex] <- n
          | _ -> ()

let seq = seq { for i = 0 to 100 do yield i }
reservoirSampling seq 5
```