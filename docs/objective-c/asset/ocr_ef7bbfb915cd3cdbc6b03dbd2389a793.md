# Creating the employee class

The purpose of this application is simply to store a list of employees and their managers. Additionally, the employee class will enable you to give the employee bonuses and raises and to calculate the employee’s age.

Additionally, there will be a special type of employee, a manager. The manager employees will have employees who report to the manager. Employees will have references to their manager so that you can access the employee’s manager. Once you’ve created the application from the template, create a new class and name it Employee. Edit the interface of that class to match Listing 3.21.

# Listing 3.21

# The Employee class interface

```
//
//  Employee.h
//  HR
//
//
//  Created by Jiva DeVoe on 4/22/10.
//  Copyright 2010 __MyCompanyName__. All rights reserved.
//

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
```