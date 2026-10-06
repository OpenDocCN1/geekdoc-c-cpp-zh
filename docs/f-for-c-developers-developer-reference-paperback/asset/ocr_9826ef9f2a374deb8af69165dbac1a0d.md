```
let mySeq5 = SimpleSequence5()

let r6 = mySeq5 (
  for i in 1..10 do
    where (i > 5 && i + 3 < 10) into j
    return j
)
```

Translation result

```
let b6 = mySeq5

b6.Bind(
  b6.Where([1..10], fun i -> b6.Return(i)),
  fun i -> i > 5 && i + 3 < 10,
  fun j -> b6.CustomOperationAttribute introduce join-like)
```

Certain properties on the CustomOperation introduce join-like operators. Listing 6-105 show how to use the IsLikeJoin property.

# LISTING 6-105 UsingLikeJoin in a computation expression

```
type SimpleStringBuilder() =
  member .For(source : seq<'a>, body : 'a -> seq<'b>) = =
    seq { v for v in source do yield! body v }
  member .Yield(item:'a) : seq<'a> = seq { yield item }

[CustomOperation("merge", IsLikeJoin = true, JoinConditionWord = "whenever") ->
  member .Merge(src1:seq<'a>, src2:seq<'a>, ks1, ks2, ret) = =
    seq { for b in src2 do
      if ks1 = ks2 then yield((ret a ) b)
    }
```

let mySeq = SimpleSequenceBuilder()

IsLikeJoin indicates that custom operation is similar to a join in a sequence computation, supporting two inputs and a correlation constraint. The expression in Listing 6-106 is translated into Listing 6-107.

# LISTING 6-106 Query code related to LikeJoin

```
myseq {
  for i in 1 .. 10 do
  merge j in [5 .. 15] whenever (i = j)
  yield j
}
```