second is the print-object command.

```
$ gdb ./a.out debug
(gdb) break debug
Breakpoint 1 at 0x100000e4d: file description.m,
  line 10.
(gdb) r
Starting program: a.out
Breakpoint 1, debug (anObject=0x100111bc0) at
  description.m:10
void anObject(id anObject) {
(gdb) print anObject
$1 = (id) 0x100111bc0
(gdb) print-object anObject
Not a very helpful message
(gdb) print-object [NSObject new]
<NSObject: 0x100111c30>
(gdb) print-object [anObject class]
DebugObject
(gdb) print-object [anObject className]
DebugObject
(gdb) print-object anObject->isa
DebugObject
```

Output from: description

This prints an object. It does this by sending a -description message to the object, which returns an NSString describing the object. This means that it will only work on valid objects. If you try using this command with objects that are prematurely deallocated or whose memory is corrupted then the debugger will either crash, or catch a segmentation violation signal.

The default implementation of this method, in NSObject, just prints the class name and