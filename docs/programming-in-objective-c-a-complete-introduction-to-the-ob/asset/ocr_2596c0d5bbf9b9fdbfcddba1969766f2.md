# Chapter 17 Memory Management

```
int main (int argc, char *argv[]) {
  NSAutleasePool *pool = [NSAutleasePool alloc] init];
  NSString *myStr1 = @"Constant string";
  NSString *myStr2 = [NSNSString stringWithString: @"string 2"];
  NSMutableString *myStr3 = [NSMutableString stringWithString: @"string 3"];
  NSMutableArray *myArr = [NSMutableArray array];

  NSLog("Retain count: myStr1: %lx, myStr2: %lx, myStr3: %lx",
        (unsigned long) [myStr1 retainCount],
        (unsigned long) [myStr2 retainCount],
        (unsigned long) [myStr3 retainCount]);

  [myArr addObject:myStr1];
  [myArr addObject:myStr2];
  [myArr addObject:myStr3];

  NSLog("Retain count: myStr1: %lx, myStr2: %lx, myStr3: %lx",
        (unsigned long) [myStr1 retainCount],
        (unsigned long) [myStr2 retainCount],
        (unsigned long) [myStr3 retainCount]);

  [myStr1 retain];
  [myStr2 retain];
  [myStr3 retain];

  NSLog("Retain count: myStr1: %lx, myStr2: %lx, myStr3: %lx",
        (unsigned long) [myStr1 retainCount],
        (unsigned long) [myStr2 retainCount],
        (unsigned long) [myStr3 retainCount]);

  // Release the reference count of myStr3 back down
  [myStr3 release];

  [pool drain];
  return 0;}
```

```
Program 17.2 Output
Retain count: myStr1: ffffffffffff, myStr2: ffffffffffff, myStr3: 1
Retain count: myStr1: ffffffffffff, myStr2: ffffffffffff, myStr3: 2
Retain count: myStr1: ffffffffffff, myStr2: ffffffffffff, myStr3: 3
```

The NSString object myStr1 is assigned the NSConstantString @*Constant string*. Space for constant strings is allocated differently in memory than for other objects. Constant strings use no reference-counting mechanism because they never be released. When the retainCount message is sent to myStr1, it returns a value of 0xffffffffffff.

Notice that the same applies to an immutable string object that is initialized with a constant string. It, too, has no meaningful retain count, as verified by the retain count displayed for myStr2.