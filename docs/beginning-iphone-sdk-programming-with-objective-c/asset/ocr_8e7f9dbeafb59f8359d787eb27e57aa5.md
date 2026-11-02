# WHAT YOU HAVE LEARNED IN THIS CHAPTER

| TOPIC | KEY CONCEPTS |
|---|---|
| Add items to a Table view | Handle the various events in the `UITableViewDataSource` protocol. |
| Allow users to select rows in a Table view | Handle the various events in the `UITableViewDelegate` protocol. |
| Add images to rows in a Table view | Use the image property of the `UITableViewCell` class and set it to an instance of the `UIImage` class containing an image. |
| Use a property list with a Table view | Use the following code snippet to locate the property list:

```objective-c
NSString *path = [[NSBundle mainBundle] pathForResource:@"Movies" ofType:@"plist"];
```

Then use a combination of `NSDictionary` and `NSArray` objects to retrieve the key/value pairs stored in the property list. |
| Group items in a Table view in sections | Implement the following methods:

- `numberOfSectionsInTableView:`
- `tableView:numberOfRowsInSection:`
- `tableView:titleForHeaderInSection:` |
| Add an index to a Table view | Implement the `sectionIndexTitlesForTableView:` method. |
| Add disclosure and checkmark images to a row in a Table view | Set the `accessoryType` property of a `UITableViewCell` object to one of the following:

- `UITableViewCellAccessoryDetailDisclosureButton`
- `UITableViewCellAccessoryCheckmark`
- `UITableViewCellAccessoryDisclosureIndicator` |
| Implement a search in a Table view | Use the Search Bar view and handle the various events in the `UISearchBarDelegate` protocol. |