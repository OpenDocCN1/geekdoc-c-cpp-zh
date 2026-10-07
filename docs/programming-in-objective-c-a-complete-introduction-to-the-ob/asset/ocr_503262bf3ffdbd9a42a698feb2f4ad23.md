```
@implementation ClassA
-(void)setStr: (NSString *) s
{
  str = s;
  [str retain];
}
```

```
-(NSString *) str
{
  return str;
}
@end
```

```
int main (int argc, char *argv[]) {
  NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
  NSMutableString *myStr = [NSMutable stringWithWith:@"A string\];
  ClassA *myA = [ClassA alloc];
  NSLog(@"myStr retain count: %lx", [myStr retainCount]);
  [myA setStr:myStr];
  NSLog(@"myStr retain count: %lx", [myStr retainCount]);
  [myStr release];
  NSLog(@"myStr retain count: %lx", [myStr retainCount]);
  [myA release];
  [pool drain];
  return 0;
}
```

# Program 17.4 Output

myStr retain count: 1
myStr retain count: 2
myStr retain count: 1

You can see that the reference count for myStr is bumped to 2 after the setStr method is invoked, this particular problem has been solved. Subsequently releasing myStr in the program makes its reference through the instance still valid because its reference count is 1.

Because you allocated myA in the program using alloc, you are responsible for releasing it yourself. Instead of worrying about releasing yourself, you could have added it to the autorelease pool by sending it an autorelease message:

[myA autorelease];

You can do this immediately after the object is allocated, if you want. Remember, adding an object to the autorelease pool doesn't release it or invalidate it; it just marks it