```
// This is the indexer for FailSoftArray.
public int this[int index] {
// This is the get accessor.
get {
if(ok(index)) {
ErrFlag = false;
return a[index];
} else {
ErrFlag = true;
return 0;
}
}

// This is the set accessor.
set {
if(ok(index)) {
a[index] = value;
ErrFlag = false;
}
else ErrFlag = true;
}
}

// Return true if index is within bounds.
private bool ok(int index) {
if(index >= 0 & index < Length) return true;
return false;
}

// Demonstrate the improved fail-soft array.
class ImprovedFSDemo {
static void Main() {
FailSoftArray fs = new FailSoftArray(5);
int x;

// Can read Length.
for(int i=0; i < fs.Length; i++)
fs[i] = i*10;

for(int i=0; i < fs.Length; i++) {
x = fs[i];
if(x != -1) Console.Write(x + " ");
}
Console.WriteLine();
// fs.Length = 10; // Error, illegal!
}
}
```

Length is now a property that uses the private variable len for its storage. Length defines only a get accessor, which means that it is read-only. Thus, Length can be read, but not