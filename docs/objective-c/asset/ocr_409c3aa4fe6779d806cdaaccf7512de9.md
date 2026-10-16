```
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