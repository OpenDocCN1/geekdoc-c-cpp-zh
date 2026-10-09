```
@implementation Person
- (float)heightInMeters
{
    return heightInMeters;
}
- (void)setHeightInMeters:(float)h
{
    heightInMeters = h;
}
- (int)weightInKilos
{
    return weightInKilos;
}
- (void)setWeightInKilos:(int)w
{
    weightInKilos = w;
}
- (float)bodyMassIndex
{
    return weightInKilos / (heightInMeters * heightInMeters);
}
@end
```

Finally, in main.m, use those methods:

```
#import "Person.h"
int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // Create an instance of Person
        Person *person = [[Person alloc] init];
        
        // Give the instance variables interesting values
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        
        // Call the bodyMassIndex method
        float bmi = [person bodyMassIndex];
        NSLog(@"person (%d, %f) has a BMI of %f",
              [person weightInKilos], [person heightInMeters], bmi);
    }
    return 0;
}
```

Build and run the program.

# ## Dot notation

Objective-C programmers call accessor methods a lot. Apple decided to create a shortcut for calling an accessor. This shortcut makes these two lines of code exactly the same: