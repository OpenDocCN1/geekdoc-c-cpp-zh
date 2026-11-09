There's more to this than first might appear. We have an array named chapters whose entries are all objects of type Chapter. Each chapter has two properties: chapterTitle and pageCount. Imagine the steps you would have to go through to create this array in the past. You would have to create the new array and copy the elements over from the old array. It's not a huge deal, but KVC makes it cleaner and easier.

But that's not all.

You can operate on these new collections and perform all sorts of calculations. The pageCount property, for example, is a number, so you can calculate the sum or the average of all the page counts in chapters. Here's how you would calculate the sum:

```
```
[self.book valueForKeyPath:@"chapters.@sum.pageCount"]
```
```

Isn't that cool? You just insert @sum before pageCount in the keypath. In general, you insert the operator between the keypath to the array and the keypath to the property.

There are two types of operators. The first type operates on a collection of numbers and returns the average, maximum, minimum, or sum (respectively, @avg, @max, @min, and @sum). The second type operates on collections and returns their @count, @distinctUnionOfArrays, @distinctUnionOfObjects, @distinctUnionOfSets, @unionOfArrays, @unionOfObjects, and @unionOfSets.

We can take some of these for a ride in our application. Declare an instance method named createReport in the BookshelfController's header file, and implement it like this:

```
```
Download KVC/Bookshelf/BookshelfController.m
```
```

```
```
- (void)createReport {
    NSLog(@"There are %@ chapters.",
        [self valueForKeyPath:@"book.chapters.@count.chapterTitle"]);
    NSLog(@"The titles are: %@",
        [self.book.chapters valueForKey:@"chapterTitle"]);
    NSLog(@"This book has %@ pages so far.",
        [self.book.chapters valueForKeyPath:@"chapters.@sum.pageCount"]);
    NSLog(@"The longest chapter is %@ pages long.",
        [self valueForKeyPath:@"book.chapters.@max.pageCount"]);
    NSLog(@"The average chapter length is %@.",
        [self.book.chapters valueForKeyPath:@"@avg.pageCount"]);
}
```
```

You might notice that again I've used different anchors for the keypaths to show you where to insert the operator. Call this method from the end of the applicationDidFinishLaunching: method in your app delegate.