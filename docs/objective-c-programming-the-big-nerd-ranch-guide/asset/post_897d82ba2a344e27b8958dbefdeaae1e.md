
#import "Person.h"
@class Asset;

@interface Employee : Person
{
    int employeeID;
    NSMutableArray *assets;
}
@property int employeeID;
- (void)addAssetsObject:(Asset *)a;
- (unsigned int)valueOfAssets;

@end

Notice the line that says `@class Asset;`. As the compiler is reading this file, it will come across the class name `Asset`. If it doesn't know about the class, it will throw an error. The `@class Asset;` line tells the compiler “There is a class called `Asset`. Don't panic when you see it in this file. That's all you need to know for now.”

Using `@class` instead of `#import` gives the compiler less information, but makes the processing of this particular file faster. You can use `@class` with `Employee.h` and other header files because the compiler doesn't need to know a lot to process a file of declarations.

Now turn your attention to `Employee.m`. With a to-many relationship, you need to create the collection object (an array, in our case) before you put anything in it. You can do this when the original object (an employee) is first created, or you can be lazy and wait until the collection is needed. Let's be lazy.

```objc
#import "Employee.h"
#import "Asset.h"

@implementation Employee

@synthesize employeeID;

- (void)addAssetsObject:(Asset *)a
{
    // Is assets nil?
    if (!assets) {
        // Create the array
        assets = [NSMutableArray alloc] init];
    }
    [assets addObject:a];
}

- (unsigned int)valueOfAssets
{
    // Sum up the resale value of the assets
    unsigned int sum = 0;
    for (Asset *a in assets) {
        sum += [a resaleValue];
    }
    return sum;
}

- (float)bodyMassIndex
{
    float normalBMI = [super bodyMassIndex];
    return normalBMI * 0.9;
}

- (NSString *)description
{
    return [NSString stringWithFormat:@"<Employee %d: $%d in assets>",
           [self employeeID], [self valueOfAssets]];
}

- (void)dealloc
{
    NSLog(@"deallocating %@", self);
}

@end
```

To process the `Employee.m` file, the compiler needs to know a lot about the **Asset** class. Thus, you imported `Asset.h` instead of using `@class`.

Also notice that you overrode **description** and **dealloc** to track the deallocation of **Employee** instances.

Build the project to see if you’ve made any mistakes.

Now you need to create some assets and assign them to employees. Edit `main.m`:

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"
#import "Asset.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // Create an array of Employee objects
        NSMutableArray *employees = [[NSMutableArray alloc] init];
        
        for (int i = 0; i < 10; i++) {
            // Create an instance of Employee
            Employee *person = [[Employee alloc] init];
            
            // Give the instance variables interesting values
            [person setWeightInKilos:90 + i];
            [person setHeightInMeters:1.8 - i/10.0];
            [person setEmployeeID:i];
            
            // Put the employee in the employees array
            [employees addObject:person];
        }
        
        // Create 10 assets
        for (int i = 0; i < 10; i++) {
            // Create an asset
            Asset *asset = [[Asset alloc] init];
            
            // Give it an interesting label
            NSString *currentLabel = [NSString stringWithFormat:@"Laptop %d", i];
            [asset setLabel:currentLabel];
            [asset setResaleValue: i * 17];
            
            // Get a random number between 0 and 9 inclusive
            NSUInteger randomIndex = random() % [employees count];
            
            // Find that employee
            Employee *randomEmployee = [employees objectAtIndex:randomIndex];
            
            // Assign the asset to the employee
            [randomEmployee addAssetsObject:asset];
        }

        NSLog(@"Employees: %@", employees);
        
        NSLog(@"Giving up ownership of one employee");
        [employees removeObjectAtIndex:5];
        
        NSLog(@"Giving up ownership of array");
        employees = nil;
    }
    return 0;
}
```

Build and run the program. You should see something like this:

```text
Employees: (
"<Employee 0: $0 in assets>",
"<Employee 1: $153 in assets>",
"<Employee 2: $119 in assets>",
"<Employee 3: $68 in assets>",
"<Employee 4: $0 in assets>",
"<Employee 5: $136 in assets>",
"<Employee 6: $119 in assets>",
"<Employee 7: $34 in assets>",
"<Employee 8: $0 in assets>",
"<Employee 9: $136 in assets>"
)
Giving up ownership of one employee
deallocating <Employee 5: $136 in assets>
deallocating <Laptop 3: $51 >
deallocating <Laptop 5: $85 >
Giving up ownership of array
deallocating <Employee 0: $0 in assets>
deallocating <Employee 1: $153 in assets>
deallocating <Laptop 9: $153 >
deallocating <Employee 9: $136 in assets>
deallocating <Laptop 8: $136 >
```

When employee #5 is removed from the array, it is deallocated because it has no owner. Then its assets are deallocated because they have no owner. (And you'll have to trust me on this: the labels (instances of `NSString`) of the deallocated assets are also deallocated once they have no owner.)

When **employees** is set to **nil**, the array no longer has an owner. So it is deallocated, which sets up an even larger chain reaction of memory clean-up and deallocation when, suddenly, none of the **employees** has an owner.

Tidy, right? As the objects become unnecessary, they are being deallocated. This is good. When unnecessary objects don’t get deallocated, you are said to have a *memory leak*. Typically a memory leak causes more and more objects to linger unnecessarily over time. The memory footprint of your application just gets bigger and bigger. On iOS, the operating system will eventually kill your application. On Mac OS X, the performance of the entire system will suffer as the machine spends more and more time swapping data out of memory and onto disk.

## Challenge

Using the **StockHolding** class from a previous challenge, make a tool that creates an instance of a **Portfolio** class and fills it with stock holdings. A portfolio can tell you what its current value is.

*This page intentionally left blank*

It is pretty common to have relationships that go in two directions. For example, maybe an asset should know which employee is currently holding it. Let's add that relationship. The new object diagram would look like this:

### Figure 20.1 Adding holder relationship

![](img/5f9368899ebf8d92fc145f8def1e89f8_135_0.png)

From a design standpoint, you would say that we are adding a pointer from the child (an instance of **Asset**) back to its parent (the instance of **Employee** that is holding it).

In *Asset.h*, add a pointer instance variable to hold on to the holding employee:

```objc
#import <Foundation/Foundation.h>
@class Employee;

@interface Asset : NSObject
{
    NSString *label;
    Employee *holder;
    unsigned int resaleValue;
}
@property (strong) NSString *label;
@property (strong) Employee *holder;
@property unsigned int resaleValue;
@end
```

In *Asset.m*, synthesize the accessors and extend the description method to display the holder:

```objc
#import "Asset.h"
#import "Employee.h"

@implementation Asset

@synthesize label, resaleValue, holder;

- (NSString *)description
{
    // Is holder non-nil?
    if ([self holder]) {
        return [NSString stringWithFormat:@"<%@: $%d, assigned to %@>",
               [self label], [self resaleValue], [self holder]];
    } else {
        return [NSString stringWithFormat:@"<%@: $%d, unassigned>",
               [self label], [self resaleValue]];
    }
}

- (void)dealloc
{
    NSLog(@"deallocating %@", self);
}

@end
```

This brings us to a style question: When people use the Asset class and Employee class together, how do we make sure that the two relationships are consistent? That is, an asset should appear in an employee’s assets array if and only if the employee is the asset’s holder. There are three options:

- Set both relationships explicitly:
  ```objc
  [vicePresident addAssetsObject:townCar];
  [townCar setHolder:vicePresident];
  ```
- In the method that sets the child’s pointer, add the child to the parent’s collection.
  ```objc
  - (void)setHolder:(Employee *)e
  {
      holder = e;
      [e addAssetsObject:self];
  }
  ```
  This approach is not at all common.
- In the method that adds the child to the parent’s collection, set the child’s pointer.

In this exercise, you will take this last option. In *Employee.m*, extend the `addAssetsObject:` method to also set `holder`.
