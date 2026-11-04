```
int lowerBound; // smallest index
int upperBound; // largest index

// An auto-implemented, read-only Length property.
public int Length { get; private set; }

// An auto-implemented, read-only Error property.
public bool Error { get; private set; }

// Construct array given its size.
public RangeArray(int low, int high) {
    high++;
    if(high <= low) {
        Console.WriteLine("Invalid Indices");
        high = 1; // create a minimal array for safety
        low = 0;
    }
    a = new int[high - low];
    Length = high - low;

    lowerBound = low;
    upperBound = --high;
}

// This is the indexer for RangeArray.
public int this[int index] {
    // This is the get accessor.
    get {
        if(ok(index)) {
            Error = false;
            return a[index - lowerBound];
        } else {
            Error = true;
            return 0;
        }
    }

    // This is the set accessor.
    set {
        if(ok(index)) {
            a[index - lowerBound] = value;
            Error = false;
        } else Error = true;
    }
}

// Return true if index is within bounds.
private bool ok(int index) {
    if(index >= lowerBound & index <= upperBound) return true;
    return false;
}
```