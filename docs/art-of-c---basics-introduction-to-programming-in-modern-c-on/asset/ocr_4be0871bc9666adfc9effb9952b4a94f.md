```
RsTopRowForW = row;
} else {
    BsTopRowForW = RsTopRowForW;
    RsTopRowForW = GsTopRowForW;
    GsTopRowForW = OsTopRowForW;
    OsTopRowForW = row;
}
return true;
}

public bool RotateBlue(bool cw = true) {
var row = RsTopRowForB;
if (cw) {
    RsTopRowForB = YsTopRowForB;
    YsTopRowForB = OsTopRowForB;
    OsTopRowForB = WsTopRowForB;
    WsTopRowForB = row;
} else {
    RsTopRowForB = WsTopRowForB;
    WsTopRowForB = OsTopRowForB;
    OsTopRowForB = YsTopRowForB;
    YsTopRowForB = row;
}
return true;
}

public bool RotateRed(bool cw = true) {
var row = GsTopRowForR;
if (cw) {
    GsTopRowForR = YsTopRowForR;
    YsTopRowForR = BsTopRowForR;
    BsTopRowForR = WsTopRowForR;
    WsTopRowForR = row;
} else {
    GsTopRowForR = WsTopRowForR;
    WsTopRowForR = BsTopRowForR;
    BsTopRowForR = YsTopRowForR;
YsTopRowForR = row;
```