
With this simple change, we display the error in the second text field.

![](img/9355405953264484a02198b0e3d25b7e_303_0.png)

Although it's nice to have this facility for dealing with unwanted input, you're better off designing an interface that doesn't allow the user to enter undefined keys. You could do this with a prepopulated drop-down list, or you could use an interface with fixed fields—one for each property you want to display.

## 19.4 Exercise: Setting Variables Using KVC

There is the setter method `setValue:forKey:` paired with the getter method `valueForKey:`. Add an action to `BookshelfController` named `setValue:`.

In this method, you set whichever property's name appears in the top text field to be the value that is entered in the bottom text field. In other words, the user is entering a key-value pair where the key (either *author* or *title*) is the contents of the top text field, and the value you are assigning that key is entered in the bottom text field.

## 19.5 Solution: Setting Variables Using KVC

Granted, this is a silly example, but it illustrates getting and setting properties using KVC. You'll need to add an outlet and an action to the `BookshelfController` header file:

```
Download KVC/Bookshelf13/BookshelfController.h

#import <Cocoa/Cocoa.h>
@class PragBook;

@interface BookshelfController : NSViewController {
    NSTextField *keyField;
    NSTextField *valueField;
    PragBook *book;
}
@property IBOutlet NSTextField *valueField, *keyField;
@property PragBook *book;

-(IBAction) getValue:(id) sender;
-(IBAction) setValue:(id) sender;
@end
```

Connect your new outlet and action in the nib file. Set your bottom text field to be selectable and editable and to send its value on Enter.

Synthesize the `keyField` property in the implementation file, and implement the `setValue:` action like this:

```
Download KVC/Bookshelf3/BookshelfController.m
- (IBAction) setValue:(id) sender {
    [self.book setValue:[sender stringValue]
                forKey:[self.keyField stringValue]];
}
```

Now you can get and set the value of any defined property as if you were using keys and values in a dictionary. Let’s take that a step further.

## 19.6 KVC and Dictionaries

So, we’ve seen that Key Value Coding lets us treat properties and their values as if they were entries in a dictionary. Let’s take a step further—it turns out to be trivial to use a dictionary to fill an object’s properties or to create a dictionary from a class so long as the keys match the names of the properties.

Let’s transform our running Bookshelf example to instantiate our PragBook and fill it with values pulled from a dictionary. This time, instead of initializing the properties in book, we create a dictionary named bookInfo with the keys title and author. We now set the values of book’s properties all at once from the bookInfo dictionary like this:

```
Download KVC/Bookshelf4/BookshelfController.m
- (PragBook *) book {
    if (!book) {
        self.book = [[PragBook alloc] init];
        NSDictionary *bookInfo =
            [NSDictionary dictionaryWithObjectsAndKeys:
                @"Manage Your Project Portfolio", @"title",
                @"Johanna Rothman", @"author", nil];
        [self.book setValuesForKeysWithDictionary: bookInfo];
    }
    return book;
}
```

That’s it.

Going the other way is only slightly more involved. We need to pass in an array that is filled with the new dictionary’s keys. These are the same as the object properties we want to capture in this dictionary. In our case, we'll capture both of them. Add this line to `setValue:` to create our dictionary and log it whenever the user changes the value of the title or author:

```
Download KVC/Bookshelf15/BookshelfController.m

-(IBAction) setValue:(id) sender {
    [self.book setValue:[sender stringValue]
        forKey:[self.keyField stringValue]];
    NSLog(@"%@", [self.book dictionaryWithValuesForKeys:
        [NSArray arrayWithObjects:@"author", @"title", nil]]);
}
```

Here I've changed the value of the author variable from Johanna Rothman to JR:

```
Bookshelf[6388:a0f] {
    author = JR;
    title = "Manage Your Project Portfolio";
}
```

Again, this example seems a little silly in this simple form, but you could easily think of cases where this facility would be useful. Imagine, for example, that you want to save your book information to disk whenever the value is changed. You already know how to read and write dictionaries to disk, and now you know how to convert a KVC-compliant class to and from a dictionary. This allows you to store and retrieve any KVC-compliant class.

## 19.7 Keypaths for Navigating a Class Hierarchy

For now our bookshelf has a single book. Now let's add a single chapter to the book. The Chapter object will have variables for storing the title and the number of pages. My goal is to show you how to traverse a hierarchy with KVC by using keypaths in place of keys.

Create a new Objective-C class named Chapter. Here's the header file:

```
Download KVC/Bookshelf16/Chapter.h

#import <Cocoa/Cocoa.h>

@interface Chapter : NSObject {
    NSString *chapterTitle;
    NSNumber *pageCount;
}
@property(copy) NSString *chapterTitle;
@property(copy) NSNumber *pageCount;
@end
```

Again, we'll do nothing more than synthesize the properties in the implementation file:

Download KVC/Bookshelf6/Chapter.m

```objc
#import "Chapter.h"

@implementation Chapter
@synthesize chapterTitle, pageCount;

@end
```

Now pop up a level and add an instance of Chapter to PragBook:

Download KVC/Bookshelf6/PragBook.h

```objc
#import <Cocoa/Cocoa.h>
@class Chapter;

@interface PragBook : NSObject {
    NSString *title;
    NSString *author;
    Chapter *chapter;
}
@property (copy) NSString *title, *author;
@property Chapter *chapter;
@end
```

Synthesize the accessors for chapter. Create and initialize chapter in PragBook's init method:

Download KVC/Bookshelf6/PragBook.m

```objc
#import "PragBook.h"
#import "Chapter.h"

@implementation PragBook
@synthesize title, author, chapter;

-(id)init {
    if (self=[super init]) {
        self.chapter = [[Chapter alloc] init];
    }
    return self;
}

-(id) valueForUndefinedKey:(NSString *)key {
    return [NSString stringWithFormat:@"No property with key %@.", key];
}
@end
```

Now our BookshelfController object has a single PragBook instance, which in turn now has a single instance of Chapter that has properties named chapterTitle and pageCount. Let's use KVC to set the values of the chapter's title and page count in the book method in BookshelfController.m. I've used setValue:forKeyPath: twice in the highlighted lines.

```objectivec
Download KVC/Bookshelf6/BookshelfController.m

-(PragBook *) book {
    if (!book) {
        self.book = [[PragBook alloc] init];
        NSDictionary *bookInfo =
            [NSDictionary dictionaryWithObjectsAndKeys:
                @"Manage Your Project Portfolio", @"title",
                @"Johanna Rothman", @"author", nil];
        [self.book setValuesForKeysWithDictionary: bookInfo];
        [self.book setValue:@"Preface"
                 forKeyPath:@"chapter.chapterTitle"];
        [self setValue:[NSNumber numberWithInt:4]
                 forKeyPath:@"book.chapter.pageCount"];
    }
    return book;
}
```

I've used two different paths just for illustration. When I start at book, I use the keypath chapter.chapterTitle. When I start at self (in other words at the BookshelfController level), the keypath is book.chapter.pageCount.

Notice that we use the method setValue:forKeyPath: where we used to use the method setValue:forKey:. You can actually view the keys as a very short keypath and use setValue:forKeyPath: in our setValue: action.

```objectivec
Download KVC/Bookshelf6/BookshelfController.m

-(IBAction) setValue:(id) sender {
    [self.book setValue:[sender stringValue]
             forKeyPath:[self.keyField stringValue]];
}
```

Similarly, the getter valueForKeyPath: is used where we used to use valueForKey:. This will let us enter keys or keypaths where before we could only enter keys.

```objectivec
Download KVC/Bookshelf6/BookshelfController.m

-(IBAction) getValue:(id) sender {
    [self.valueField setStringValue:
        [self.book valueForKeyPath:[sender stringValue]]];
}
```

So now, in addition to entering the author and title keys in the top text field, we can safely use the keypaths "chapter.chapterTitle" and "chapter.pageCount" to get and set those values as well.
