```
"@FoofloatVal];
  return self;
}
@end
```

The encoding routine first encodes the string value strVal using the encodeObject:forKey method, as was shown previously.

In Program 19.8, a Foo object is created, archived to a file, unarchived, and then displayed.

# Program 19.8. Test Program

```
#import <Foundation/Foundation.h>
#import "Foo.h" // Definition for our Foo class

int main (int argc, char * argv[]) {
  @autoreleasepool {
    Foo *myFoo = [[Foo alloc init];
    Foo *myFoo2;

    [myFoo setStrVal: @"This is the string\];
    [myFoo setIntVal: 12345];
    [myFoo setFloatVal: 98.6];

    [NSKeyedArchiver archiveRootObject:myFooToFile:@"foo.arch\];

    myFoo2 = [NSKeyedUnarchiver unarchiveObjectWithFile:@"foo.arch\];
    NSLog(@"%@\n%i\n%g", [myFoo2 strVal], *)
```