# Listing 3.12

# The employee class interface

```
#import <Cocoa/Cocoa.h>

@interface Employee : NSObject
{
    NSString *firstName;
    NSString *lastName;
    NSDate *birthDate;
    NSDate *dateOfEmployment;
    Employee *manager;
    NSString *ssn;

    double salary;
}
@property (nonatomic, retain) NSString * firstName;
@property (nonatomic, retain) NSString * lastName;
@property (nonatomic, retain) NSDate * birthDate;
@property (nonatomic, retain) NSDate * dateOfEmployment;
@property (nonatomic, assign) Employee * manager;
@property (nonatomic, retain) NSString * ssn;
@property (nonatomic, readonly) NSTimeInterval age;
@property (nonatomic) double salary;

-(id)initWithFirstName:(NSString *)inFirstName lastName:(NSString *)inLastName birthDate:(NSDate *)inBirthDate ssn:(NSString *)inSsn;
-(id)init;
-(void)giveRaise:(double)percentage;
-(double)bonus;

@end
```

The first thing to note is that almost all the properties specified here have data members that they map to. A property declaration consists of the @property directive followed by attributes that affect the type of accessor that is created as part of this property. These attributes are specified inside the parentheses after the @property directive. The different attributes that can be specified for a given property are shown in Table 3.1.