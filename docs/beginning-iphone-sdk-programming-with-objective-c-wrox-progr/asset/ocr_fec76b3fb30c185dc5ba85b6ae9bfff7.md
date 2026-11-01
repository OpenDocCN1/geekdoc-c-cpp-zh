+   3. Name the property list as Apps.plist.
+   4. Populate the Apps.plist as shown in Figure 13-5.

![](bbox=[0.15, 0.22, 0.55, 0.53])

FIGURE 13-5

In the viewDidLoad method, add the following statements that appear in bold:

```
```objc
- (void)viewDidLoad {
    //---filename---
    NSString *fileName = [[self documentsPath]
        stringByAppendingPathComponent:@"data.txt"];
    //---write something to the file---
    [self writeToFile:@"a string of text" withFileName:fileName];
    //---read it back---
    NSString *fileContent = [self readFromFile:fileName];
    //---display the content read in the Debugger Console window---
    NSLog(fileContent);
    //---get the path to the property list file---
    NSString *plistFileName = [[self documentsPath]
        stringByAppendingPathComponent:@"Apps.plist"];
```
```