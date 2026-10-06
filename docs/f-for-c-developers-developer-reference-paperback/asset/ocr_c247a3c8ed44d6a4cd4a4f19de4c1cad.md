Translation result
let b = mySeq
b.For ([1..10], fun i -> b.Yield(i * i))

The where operation is introduced by the CustomOperation attribute, which is shown in Listing 6-100. The ProjectionParameter on the second parameter is useful to simplify the function definition. Lacking this attribute, the where part in the computation expression has to be written as fun i -> explicitly. The ProjectionParameter is useful when there is a let binding between the customer operator and ForEach, like the one shown in Listing 6-101.

# LISTING 6-100 Using CustomOperation and ProjectionParameter attributes

```
type SimpleSequence2() = =
  member.For(source:seq<'a>, f:a -> seq<'b>) = =
    seq (n in source yield! f n)
  member.Yield(n) = seq { yield n }
<CustomOperation('where')>=
  member.Where(source:seq<'a>, [ProjectionParameter])f:a -> bool) = =
    source | Seq.Filter f
```

```
let mySeq2 = SimpleSequence2()
let r2 = mySeq2 {
  for i in 1..10 do
    where (i > 3)
}
```

```
Translation result
let b2 = mySeq2
b2.Where (b.For([1..10], fun i -> b.Yield(i)), fun i-> i)
```

# LISTING 6-101 ProjectParameter and let binding

```
let r3 = mySeq2 {
  for i in 1..10 do
    let j = i + 3
    where (i > 5 && j < 10)
}
```

```
Translation result
let b3 = mySeq2
b3.Where(b.For([1..10], fun i ->
  let j = i + 3
  b.Yield(i, j)),
fun (i, j) -> i > 5 && j < 10)
```