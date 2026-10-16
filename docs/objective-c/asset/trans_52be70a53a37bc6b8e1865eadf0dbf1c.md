

## Listing 3.21 (continued)

```
@property (nonatomic, retain) NSDate * dateOfEmployment;
@property (nonatomic, assign) Employee * manager;
@property (nonatomic, retain) NSString * ssn;
@property (nonatomic, readonly) NSTimeInterval age;
@property (nonatomic) double salary;

-(id)initWithFirstName:(NSString *)inFirstName
    lastName:(NSString *)inLastName
    birthDate:(NSDate *)inBirthDate
    ssn:(NSString *)inSsn;
-(void)giveRaise:(double)percentage;
-(double)bonus;

@end
```

请注意，此文件的接口为员工类可能需要跟踪的所有属性定义了各种数据成员。此外，我们还定义了属性来访问这些数据成员。请注意，其中一些属性，例如 age 属性，并不直接映射到数据成员，而是最终会成为计算值。

大多数属性都使用了 retain 属性。例外情况包括标量值属性、计算属性（为只读）以及 manager 属性。在本例中，manager 属性将是一个特殊情况。manager 属性将拥有一个向其汇报的员工列表。因为将员工添加到该汇报列表中会使经理保留这些员工，所以你不希望员工上的 manager 属性也被保留。我将在下一章关于内存管理的章节中解释更多原因。现在，只需理解员工上的 manager 属性应设置为 assign 属性而不是 retain 属性。

在创建完接口文件后，继续编辑实现文件。使其与 Listing 3.22 中的代码相匹配。

## Listing 3.22
### The employee class implementation file

```
//
// Employee.m
// HR
//
//  Created by Jiva DeVoe on 4/22/10.
//  Copyright 2010 __MyCompanyName__. All rights reserved.
//

#import "Employee.h"

@implementation Employee
@synthesize firstName;
@synthesize lastName;
@synthesize birthDate;
@synthesize dateOfEmployment;
@synthesize manager;
@synthesize ssn;
@synthesize salary;
@dynamic age;

-(void)dealloc
{
    [self setFirstName:nil];
    [self setLastName:nil];
    [self setBirthDate:nil];
    [self setDateOfEmployment:nil];
    [self setSsn:nil];
    [self setManager:nil];

    [super dealloc];
}

-(id)init;
{
    if(self = [super init])
    {
    }
    return self;
}

-(id)initWithFirstName:(NSString *)inFirstName
    lastName:(NSString *)inLastName
    birthDate:(NSDate *)inBirthDate
    ssn:(NSString *)inSsn;
{
    if(self = [self init])
    {
```

## Listing 3.22 (continued)

```
[self setFirstName:inFirstName];
[self setLastName:inLastName];
[self setBirthDate:inBirthDate];
[self setSsn:inSsn];
}
return self;
}
-(NSTimeInterval)age;
{
    return [birthDate timeIntervalSinceNow];
}
-(void)giveRaise:(double)percentage;
{
    salary = salary + (salary * percentage);
}
-(double)bonus;
{
    return salary * .05;
}
@end
```

这里需要注意的重要事项是，首先，有一个接受多种参数的初始化方法，用于初始化 Employee 类的成员变量。通过使用此初始化方法，你创建的对象将具有所有基本属性已初始化并准备就绪。

在此代码中需要注意的另一件重要事项是我们为计算员工年龄的目的创建了一个动态属性。为此，我们对 age 属性使用了 @dynamic 指令。然后我们创建一个 age 访问方法，该方法使用员工的出生日期计算年龄。这里还定义了两个方法，一个用于给员工加薪，另一个用于给员工发放奖金。这两个方法将在我们的 manager 类中被重写，以提供不同的加薪和奖金百分比。

## Creating the manager class

现在你已经创建了 Employee 类，你需要创建一个名为 Manager 的 Employee 类的子类。此类有一个向该员工汇报的员工列表，并且有不同的加薪和奖金百分比。

要创建 manager 类，向你的项目添加一个新类文件，将其命名为 Manager，并编辑每个接口文件以匹配 Listing 3.23。

## Listing 3.23
### The Manager class interface

```
#import <Cocoa/Cocoa.h>
#import "Employee.h"

@interface Manager : Employee
{
    NSMutableArray *reports;
}
@property (nonatomic, retain) NSMutableArray * reports;

- (void)addReport:(Employee *)inEmployee;

@end
```

请记住，为了创建一个从另一个类继承的类，你需要在接口操作中在类名之后指定父类。正如你从此代码中看到的那样，你就是这样做的。通过这样做，请记住 Manager 类将继承其父类 Employee 类的所有属性和行为。

当涉及到 Manager 类的不同之处时，你需要在此处指定这些项目。具体来说，你需要添加 reports 数组来存储将向此经理汇报的员工。此外，这里有一个用于向经理的汇报列表中添加汇报的方法。切换到 Manager 实现文件，将其编辑为如下所示 Listing 3.24。

## Listing 3.24
### Manager implementation file

```
#import "Manager.h"

@implementation Manager
@synthesize reports;

- (void)dealloc
{
```

## Listing 3.24 (continued)

```
for (Employee *employee in reports)
{
    [employee setManager:nil];
}

[self setReports:nil];
[super dealloc];
}

-(id)init;
{
    if (self = [super init])
    {
        [self setReports:[NSMutableArray array]];
    }
    return self;
}

-(void)addReport:(Employee *)inEmployee;
{
    [reports addObject:inEmployee];
    [inEmployee setManager:self];
}

-(double)bonus;
{
    return salary * .10;
}

@end
```

关于此代码需要注意的重要事项是，我们在这里有一个指定初始化方法，它创建 reports 数组并对其进行初始化。此指定初始化方法将在 Employee 类的初始化方法被调用时从 Employee 类调用。如果你参考 Employee 类的实现文件，你会看到对 [super init] 的调用，该调用调用此方法。请注意，bonus 方法也在此类中被重写。这是为了使授予员工的奖金金额与标准员工的奖金金额采用不同的百分比。

最后需要注意的一点是，在 dealloc 方法中，manager 对象遍历其 reports，并在其被释放时将其自身从这些 reports 的 manager 中移除。请记住，员工上的 manager 属性是使用 assign 属性而不是 retain 属性设置的。其结果是，如果 manager 对象被分配但向该 manager 汇报的员工未被分配，则员工中引用 manager 的指针将变得无效。因此，当 manager 释放自身时，让 manager 将其 reports 上的 manager 属性设置为 nil 是很重要的。这是未来在处理委托时需要记住的重要模式。

## Tying the classes together in the HR main

现在你已经看到了员工和经理类定义，我想展示如何创建这些类的实例并将它们联系起来。

如果将示例应用程序的主过程编辑为如下所示 Listing 3.25，则它将演示现在我们拥有这些类后可以执行的一些基本操作。

## Listing 3.25

```
#import <Foundation/Foundation.h>
#import "Employee.h"
#import "Manager.h"

int main (int argc, const char * argv[])
{
    NSAutoreleasePool * pool = [[NSAutoreleasePool alloc] init];

    Employee *joeBlow = [[Employee alloc]
                        initWithFirstName:@"Joe"
                                  lastName:@"Blow"
                                 birthDate:
                        [NSDate dateWithNaturalLanguageString:@"12/01/1990"]
                                       ssn:@"555-12-1212"];

    Employee *janeDoe = [[Employee alloc]
                        initWithFirstName:@"Jane"
                                  lastName:@"Doe"
                                 birthDate:
                        [NSDate dateWithNaturalLanguageString:@"11/01/1985"]
                                       ssn:@"555-12-1212"];

    Manager *johnAppleseed = [[Manager alloc]
                             initWithFirstName:@"John"
                                   lastName:@"Appleseed"
                                  birthDate:
                        [NSDate dateWithNaturalLanguageString:@"11/01/1970"]
                                       ssn:@"555-12-1212"];
    [johnAppleseed addReport:joeBlow];
```
