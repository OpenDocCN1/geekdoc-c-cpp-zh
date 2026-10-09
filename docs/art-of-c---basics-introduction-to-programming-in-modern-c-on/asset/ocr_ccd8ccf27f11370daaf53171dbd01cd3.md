```
set => B.RightCol = value;
}
private Triplet WsTopRowForO {
    get => W.LeftCol;
    set => W.LeftCol = value;
}
private Triplet GsTopRowForO {
    get => G.LeftCol;
    set => G.LeftCol = value;
}
private Triplet YsTopRowForO {
    get => Y.RightCol;
    set => Y.RightCol = value;
}
private Triplet BsTopRowForY {
    get => B.BottomRow;
    set => B.BottomRow = value;
}
private Triplet OsTopRowForY {
    get => O.BottomRow;
    set => O.BottomRow = value;
}
private Triplet GsTopRowForY {
    get => G.BottomRow;
    set => G.BottomRow = value;
}
private Triplet RsTopRowForY {
    get => R.BottomRow;
    set => R.BottomRow = value;
}
public bool RotateWhite(bool cw = true) {
    var row = BsTopRowForW;
    if (cw) {
        BsTopRowForW = OsTopRowForW;
        OsTopRowForW = GsTopRowForW;
        GsTopRowForW = RsTopRowForW;
```