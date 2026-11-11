
```objectivec
Download Multithreading/PPImportOperation.m

NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
for (NSManagedObject *recipe in incomingRecipes) {
    [self copyRecipe:recipe];
    [pool drain];
    pool = nil;
    pool = [[NSAutoreleasePool alloc] init];
}
[pool drain];
pool = nil;
```

Once we have all the recipes, we need to loop over them and copy each one to the main NSManagedObjectContext. This copy operation is fairly complicated, but the basic flow is this:

- 1. Copy the Recipe entity and its property attributes.
- 2. Copy each relationship, searching for existing objects by name if they are not RecipeIngredients. If they are RecipeIngredients, copy them without searching.
- 3. For each object in the relationship, copy its relationships, taking care to never copy parent objects.

This copy is one-way, as discussed in the sidebar on page 171. Once the copy is complete, we need to save the main NSManagedObjectContext and get ready to update the main thread and its NSManagedObjectContext.

```objectivec
Download Multithreading/PPImportOperation.m

error = nil;
if (![[self mainContext] save:&error]) {
    [NSApp presentError:error];
    return;
}
```

Once we have completed the import, it is time to save the context and confirm that it was successful. Once the save is complete, we can exit the -main method and complete the NSOperation. The only question that remains is: how do we update the main NSManagedObjectContext and thereby the UI?

When we wrote the -initWithDelegate:filePath:, we added the NSOperation as an observer to its own NSManagedObjectContextDidSaveNotification broadcasts. When we performed the -save: in the -main method, the notification was automatically fired. To update the main NSManagedObjectContext, we need to forward that notification along.

```objectivec
id oldDestObject = nil;
id temp = nil;
NSDictionary *relationships = [[oldObject entity] relationshipsByName];
for (NSString *key in [relationships allKeys]) {
    NSRelationshipDescription *relationship = [relationships objectForKey:key];
    NSString *destEntityName = [[relationship destinationEntity] name];
    if ([destEntityName isEqualToString:parentEntity]) continue;

    if ([relationship isToMany]) {
        NSMutableSet *newDestSet = [NSMutableSet set];
        for (id oldDestObject in [oldObject valueForKey:key]) {
            temp = [[self lookup] objectForKey:[oldDestObject objectID]];
            if (!temp) {
                temp = [self associateObject:oldDestObject
                                      parent:entityName];
            }
            [newDestSet addObject:temp];
        }
        [newObject setValue:newDestSet forKey:key];
    } else {
        oldDestObject = [oldObject valueForKey:key];
        if (!oldDestObject) continue;
        temp = [[self lookup] objectForKey:[oldDestObject objectID]];
        if (!temp) {
            temp = [self associateObject:oldDestObject
                                  parent:entityName];
        }
        [newObject setValue:temp forKey:key];
    }
}
```

The second half of the copy is quite a bit more complicated. The first issue is that a relationship can be pointing to one object or multiple objects, and each of those possibilities needs to be handled differently. Second, the object on the other end of that relationship may or may not exist. If the destination object exists, then we can just set the relationship. If it does not exist, then we need to create it, which is done in the -associateObject:parent: method discussed in a moment. It is here that we use the lookup dictionary. By using the NSManagedObjectID as the key, we can ensure that different relationships pointing to the same object remain intact.

One important thing to note here is the parentEntity variable that is being passed in. This variable is checked at the start of each relationship copy. If the destination object for that relationship matches this variable, then the relationship is skipped. This guarantees that the copy is performed only down the tree and never back up.

## -associateObject:parent:

This method is called from the -copyPropertiesFromObject:toObject:parent: method whenever it fails to find a destination object in the lookup dictionary.

```objectivec
Download Multithreading/PPImportOperation.m

- (id)associateObject:(NSManagedObject*)object parent:(NSString*)name
{
    NSManagedObjectContext *moc = [self mainContext];
    NSString *entityName = [[object entity] name];
    id temp = nil;

    if ([entityName isEqualToString:@"RecipeIngredient"]) {
        temp = [NSEntityDescription insertNewObjectForEntityForName:entityName
                                    inManagedObjectContext:moc];
        [[self lookup] setObject:temp forKey:[object objectID]];
        [self copyPropertiesFromObject:object toObject:temp parent:name];
        return temp;
    }

    if (temp = [self objectOfType:entityName
                withName:[object valueForKey:@"name"]]) {
        [[self lookup] setObject:temp forKey:[object objectID]];
        return temp;
    }

    temp = [NSEntityDescription insertNewObjectForEntityForName:entityName
                                inManagedObjectContext:moc];
    [[self lookup] setObject:temp forKey:[object objectID]];
    [self copyPropertiesFromObject:object toObject:temp parent:name];
    return temp;
}
```

In this method, unlike the previous method discussed, we care what kind of entity we are working with. If we are working with a RecipeIngredient, then we know to just blindly create a new object. However, for any other object, we need to first check to see whether it already exists in the NSManagedObjectContext. We do this by calling -objectOfType:withName:, and if it returns a nil, then we need to create a new object. If it returns an NSManagedObject, then we associate that returned object with the original object passed in so that future calls against it will be found in the lookup dictionary.

There are a couple of things to note. First, no matter whether we are creating a new object or associating an existing object, we always store the reference in our lookup dictionary. This makes sure we do not duplicate the work and that we can refresh the object later as needed.

The other important thing to note here is the recursion. If we create a new object, we call copyPropertiesFromObject:toObject:parent: on that object even though that is the method that we just came from. However, because of the parent reference, we guarantee that the copy loop never goes back up the chain.

## -objectOfType:withName:

The final method in this copy routine is called from the -associateObject:parent: method. This method determines whether an object already exists in the NSManagedObjectContext to avoid duplication.

```objectivec
Download Multithreading/PPImportOperation.m

- (id)objectOfType:(NSString*)entityName withName:(NSString*)name
{
    NSFetchRequest *request = [[NSFetchRequest alloc] init];
    [request setEntity:[NSEntityDescription entityForName:entityName
                                       inManagedObjectContext:[self mainContext]]];
    [request setPredicate:[NSPredicate predicateWithFormat:@"name == %@", name]];

    NSError *error = nil;
    id result = [[[self mainContext] executeFetchRequest:request
                                                   error:&error] lastObject];

    return result;
}
```

In our data model, almost every object has a name property. Fortunately, in the one case that this is not true, we don’t care whether there are duplicate objects. Therefore, this method gets rather heavily used during the import operation to help guarantee that we are not creating more than one object with the same name.

We accomplish this check by creating an NSFetchRequest using the name as the test in the predicate and passing the passed-in entityName to construct the NSEntityDescription. We then return the -lastObject of the NSArray returned from the fetch. By using -lastObject, we can avoid having to check the length of the returned array. -lastObject will check the length for us automatically and return a nil if the NSArray has no objects.
