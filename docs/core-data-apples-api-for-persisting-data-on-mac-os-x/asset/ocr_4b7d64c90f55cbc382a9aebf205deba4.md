Download RecipeCT/Classes/RecipeDetailViewController.m

```
- (void)setEditing:(BOOL)editing animated:(BOOL)animated
{
    [super setEditing:editing animated:animated];
    [self.navigationItem setHidesBackButton:editing animated:YES];

    [[self titleLabel] setEnabled:editing];

    if (editing) return;
    NSManagedObjectContext *context = recipe.managedObjectContext;
    NSError *error = nil;
    if (![context save:&error]) return;

    NSLog(@"save error %@, %@", error, [error userInfo]);
    exit(-1); // Fail
}
```

Because we are using an NSFetchedResultsController, it automatically monitors the NSManagedObjectContext for changes and broadcasts them to its delegate. Therefore, a simple save of the NSManagedObjectContext automatically takes care of any change notifications in the other view controllers.

# Overview

In this section, we looked into the impacts that adding Core Data to a Cocoa Touch application has. Similar to the desktop, Core Data helps to eliminate a large portion of the code dealing with the object hierarchy and persisting data to disk. By adding Core Data to a Cocoa Touch project, we can further reduce the amount of code required to develop an application and reduce the time to market even further.

# 10.5 Going Further

Because of our focus purely on Core Data in this chapter, we did not cover all aspects of this application. We also did not complete the application and make it consumer ready.

Interestingly enough, with the release of v3.0 for Cocoa Touch, Apple also released a sample recipes application for the iPhone that uses Core Data. This application is available to everyone who has an iPhone developer account, and I highly recommend reviewing the solutions provided in that project.