```
```
} 
    return true; 
} 

public bool RotateGreen(bool cw = true) {
    var row = OsTopRowForG; 
    if (cw) {
        OsTopRowForG = YsTopRowForG; 
        YsTopRowForG = RsTopRowForG; 
        RsTopRowForG = WsTopRowForG; 
        WsTopRowForG = row; 
    } else {
        OsTopRowForG = WsTopRowForG; 
        WsTopRowForG = RsTopRowForG; 
        RsTopRowForG = YsTopRowForG; 
        YsTopRowForG = row; 
    }
    return true;
} 

public bool RotateOrange(bool cw = true) {
    var row = BsTopRowFor0; 
    if (cw) {
        BsTopRowFor0 = YsTopRowFor0; 
        YsTopRowFor0 = GsTopRowFor0; 
        GsTopRowFor0 = WsTopRowFor0; 
        WsTopRowFor0 = row; 
    } else {
        BsTopRowFor0 = WsTopRowFor0; 
        WsTopRowFor0 = GsTopRowFor0; 
        GsTopRowFor0 = YsTopRowFor0; 
        YsTopRowFor0 = row; 
    }
    return true;
} 

public bool RotateYellow(bool cw = true) {
    var row = BsTopRowForY;
```
```