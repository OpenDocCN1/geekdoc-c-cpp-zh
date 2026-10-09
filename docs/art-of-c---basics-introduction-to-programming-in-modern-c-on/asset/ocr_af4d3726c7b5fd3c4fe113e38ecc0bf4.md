```
            _ => false,
           };
      }
}
```

# rubiks-cube/Cube.cs (lines 47-62)

```
private Triplet BsTopRowForW {
    get => B.TopRow;
    set => B.TopRow = value;
}
private Triplet RsTopRowForW {
    get => R.TopRow;
    set => R.TopRow = value;
}
private Triplet GsTopRowForW {
    get => G.TopRow;
    set => G.TopRow = value;
}
private Triplet OsTopRowForW {
    get => O.TopRow;
    set => O.TopRow = value;
}
```