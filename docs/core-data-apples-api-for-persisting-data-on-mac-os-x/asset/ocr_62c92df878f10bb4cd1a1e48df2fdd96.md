In this code segment, we first retrieve the metadata from the source URL. If that metadata is not nil, we ask the final model whether the metadata is compatible with it. If it is, then we are happy and done. We then set the error pointer to nil and return YES. If not, then we need to try to figure out the mapping model and potentially the interim data model to migrate to.

# ### Finding All the Managed Object Models

To find the next step in the migration, we need to find every managed object model in the bundle and loop through them. The goal at this point is to get all the models and then figure out which one we can migrate to. Since these models will probably be in their own bundles, we have to first look for the bundles and then look inside each of them.

```
```objective-c
// Download ProgressiveMigration/AppDelegate.m
//Find the source model
NSManagedObjectModel *sourceModel = [NSManagedObjectModel
        mergedModelFromBundles:nil
        forStoreMetadata:sourceMetadata];
NSAssert(sourceModel != nil, ([NSString stringWithFormat:
        @"Failed to find source model\n%@",
        sourceMetadata]));

//Find all of the mom and momd files in the Resources directory
NSMutableArray *modelPaths = [NSMutableArray array];
NSArray *momdArray = [[NSBundle mainBundle] pathsForResourcesOfType:@"momd"
        inDirectory:nil];

for (NSString *momdPath in momdArray) {
    NSString *resourceSubpath = [momdPath lastPathComponent];
    NSArray *array = [[NSBundle mainBundle]
        pathsForResourcesOfType:@"mom"
        inDirectory:resourceSubpath];
    [modelPaths addObjectsFromArray:array];
}

NSArray* otherModels = [[NSBundle mainBundle] pathsForResourcesOfType:@"mom"
        inDirectory:nil];
[modelPaths addObjectsFromArray:otherModels];

if (!modelPaths || ![modelPaths count]) {
    //Throw an error if there are no models
    NSMutableDictionary *dict = [NSMutableDictionary dictionary];
    [dict setValue:@"No models found in bundle"
        forKey:NSLocalizedDescriptionKey];
    //Populate the error
    *error = [NSError errorWithDomain:@"Zarra" code:8001 userInfo:dict];
    return NO;
}
```
```