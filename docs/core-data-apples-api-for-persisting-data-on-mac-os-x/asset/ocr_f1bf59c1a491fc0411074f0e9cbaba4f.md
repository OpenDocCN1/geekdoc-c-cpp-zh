![](bbox=[0.325, 0.081, 0.581, 0.202])

Figure 12.1: Parameter table model

a dynamic number of accessors. However, we do not want to have to write an accessor every time that we add a parameter: ideally, we want to just call -valueForKey: and -setValue:forKey: and not worry about the persistence of these values. Lastly, we want to be able to set up some default values.

An important point about the defaults is that they are not persisted to disk. If they get persisted, then later versions that change the default would require additional code to check for persisted defaults and reset them. If, however, we do not persist them, then users of newer versions of the application automatically get the newer defaults for free and, more important, do not get their preferences destroyed if they have changed the value from its default.

The DocumentPreferences object will accomplish all of these goals:

Download CDPreferences/DocumentPreferences.h

```
```objc
@interface DocumentPreferences : NSObject
{
    NSDictionary *_defaults;
    NSPersistentDocument *_associatedDocument;
}

@property (assign) NSPersistentDocument *associatedDocument;
@property (assign) NSDictionary *defaults;

- (id)initWithDocument:(NSPersistentDocument*)associatedDocument;
- (NSArray*)allParameterNames;
- (NSDictionary*)allParameters;

@end
```
```