Download `KVC/Bookshelf8/BookshelfAppDelegate.m`

```
```objective-c
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    BookshelfController * bc = [[BookshelfController alloc]
                                  initWithNibName:@"Bookshelf" bundle:nil];
    [self.window setContentSize:[bc.view bounds].size];
    [self.window setContentView:bc.view];
    [bc createReport];
}
```
```

Click Build & Run, and you should see something like this in your Console:

```
```text
There are 5 chapters.
The titles are: (
    "Preface",
    "Meet Your Project Portfolio",
    "Create Your First Draft",
    "Evaluate Your Projects",
    "Rank the Portfolio"
)
This book has 59 pages so far.
The longest chapter is 20 pages long.
The average chapter length is 11.8.
```
```

So, have I convinced you? Can you see that KVC is about much more than replacing [foo bar] with [foo valueForKey:@"bar"]? You can read more about KVC in Apple’s *Key-Value Coding Programming Guide* [App08].

KVC brings you a lot of flexibility, but that’s only the half of it. The real power of KVC is in the other technologies that it enables. In the next chapter, we’ll look at the other foundational piece of this puzzle: Key Value Observing.