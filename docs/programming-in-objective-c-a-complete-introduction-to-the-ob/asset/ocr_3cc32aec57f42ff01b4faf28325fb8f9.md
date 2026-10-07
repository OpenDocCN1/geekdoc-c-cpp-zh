# AddressBook Interface File

```
#import <Foundation/Foundation.h>
#import "AddressCard.h"
```

```
@interface AddressBook: NSObject <NSCopying, NSCopying>
{
    NSString *bookName;
    NSMutableArray *book;
}
```

```
@property (nonatomic, copy) NSString *bookName;
@property (nonatomic, copy) NSMutableArray *book;
```

```
-(id) initWithName:(NSString *) name;
-(void) sort;
-(void) addCard:(AddressCard *) theCard;
-(void) sort2;
-(void) removeCard:(AddressCard *) theCard;
-(int) entries;
-(void) list;
-(AddressCard *) lookup:(NSString *) theName;
```

```
@end
```

# AddressCard Implementation File

```
#import "AddressCard.h"
```

```
@implementation AddressCard
```

```
@synthesize name, email;
```

```
-(void) setName:(NSString *) theName andEmail:(NSString *) theEmail
{
    self.name theName;
    self.email theEmail;
}
```

```
// Compare the two names from the specified address cards
-(NSComparisonResult) compareNames:(id) element
{
    return [name] compare:[element name]];
}
```