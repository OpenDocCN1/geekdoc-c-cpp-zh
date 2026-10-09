```
36 return true;
37 }
38 return false;
39 }

public bool SetCode(string newCode, string currentCode) {
    if
    (crypto.ComputeHash(Encoding.ASCII.GetBytes(currentCode)).ToHex() ==
    hash) {
        if (!IsCodeInValidFormat(newCode)) {
            return false;
        }
        hash =
        crypto.ComputeHash(Encoding.ASCII.GetBytes(newCode)).ToHex();
        State = LockState.Locked;
        return true;
    }
    return false;
}

private static bool IsCodeInValidFormat(string code) {
    if (string.IsNullOrEmpty(code) || code.Trim() != code) {
        return false;
    }
    return ulong.TryParse(code, out ulong _);
}
```

Note that DoorLock inherits the behavior of IDisposable, which we used in some earlier lessons.

The door lock state, LockState, is defined as an enum: