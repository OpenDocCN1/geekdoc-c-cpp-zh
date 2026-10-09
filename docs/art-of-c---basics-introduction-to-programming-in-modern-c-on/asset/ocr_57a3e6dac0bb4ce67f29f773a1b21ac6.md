# rubiks-cube/Cube.cs (lines 149-163)

```
public bool RotateWhite(bool cw = true) {
    var row = BsTopRowForW;
    if (cw) {
        BsTopRowForW = OsTopRowForW;
        OsTopRowForW = GsTopRowForW;
        GsTopRowForW = RsTopRowForW;
        RsTopRowForW = row;
    } else {
        BsTopRowForW = RsTopRowForW;
        RsTopRowForW = GsTopRowForW;
        GsTopRowForW = OsTopRowForW;
        OsTopRowForW = row;
    }

    return true;
}
```

# rubiks-cube/Cube.cs (lines 245-257)

```
public override string ToString() {
    var range = new List<int>() { 0, 1, 2 };
    var sb = new StringBuilder();
    sb.AppendLine(string.Concat(Repeat(new string('-', 7) + " ", 6)));
    foreach (var i in range) {
        for (var f = 0; f < 6; f++) {
            sb.Append($"[{string.Join(' ', range.Select(j => faces[f].GetRow(i)[j]).ToArray()}]");
        }
        sb.AppendLine();
    }
    sb.Append(string.Concat(Repeat(new string('-', 7) + " ", 6)));

    return sb.ToString();
}
```