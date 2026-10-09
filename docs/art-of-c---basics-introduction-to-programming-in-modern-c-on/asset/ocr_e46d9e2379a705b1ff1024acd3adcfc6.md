```
list.RemoveAt(list.Count - 1);
return tok;
}
return default;
}

public bool TryPop(out T? tok) {
if (list.Count > 0) {
tok = list[^1];
list.RemoveAt(list.Count - 1);
return true;
}
tok = default;
return false;
}

public T PopOrDie() {
if (list.Count > 0) {
var tok = list[^1];
list.RemoveAt(list.Count - 1);
return tok;
}
throw new IndexOutOfRangeException();
}

public (bool, T?) PopSoft() {
if (list.Count > 0) {
var tok = list[^1];
list.RemoveAt(list.Count - 1);
return (true, tok);
}
return (false, default);
}
```

This stack implementation uses System.Collections.Generic.List<T> to store the internal data (through "composition"), and it exposes the conventional Push()