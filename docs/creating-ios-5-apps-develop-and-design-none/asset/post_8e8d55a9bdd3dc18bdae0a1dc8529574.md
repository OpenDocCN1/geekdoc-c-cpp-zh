
## 6 LOADING AND SAVING DATA

Always remember, iOS is not a desktop operating system. Some of the things we take for granted on desktop machines are impossible, inappropriate, or at least very difficult in iOS. The file system is a great example of this. Where the desktop often displays dialog boxes to open and save files, forcing the user to search through a forest of directories, iOS goes to great lengths to hide the underlying file system, both from the user and from the applications themselves.

This provides two main benefits. For the user, this greatly simplifies the experience. You don’t need to worry about where files are stored or how to find them. Your application handles all of this transparently. For the applications, limiting access to the file system greatly improves system security. Each application is limited to its own sandbox. The application can freely open and save files within this sandbox, but it cannot touch anything outside these carefully defined boundaries. This protects both your data and the system files from accidental (or worse yet, malicious) alterations. Unfortunately, it also makes sharing files between applications somewhat difficult. The communication channels between applications are few and tightly controlled.

### GENERATING DIRECTORY PATHS

Within the application sandbox, iOS sets aside specific directories for different types of use. These include the Document, Temporary, Caches, and Application Support directories.

The Document directory stores our application’s documents—basically, any user-generated data. When writing a text editor, this is where we save the user’s text files. When designing a game, this is where we store the saved game files. For Health Beat, this is where we save our WeightHistory.

The Temporary directory provides a handy location for storing information that does not need to survive past the current session. This often includes the scratch space needed for large calculations and similar transient uses. It’s best to actively delete these files when they are no longer needed; however, the system will periodically clear out the Temporary directory when our application is not running.

The Caches directory also stores temporary information; however, this directory focuses on caching data to improve performance. Most of the time this means saving information that we may need to reuse, especially information that takes a long time or a lot of computational effort to re-create.

You are probably familiar with caches from Web browsers. The browser caches a page after downloading it. The next time you try to view that page, it simply loads the file from disk instead of downloading it again.

Caches also differ from temporary files in one other important way—caches typically persist beyond the current session. After all, a Web browser doesn’t clear out its cache each time it launches. However, this data may be automatically deleted if the device is running out of disk space, so we cannot depend on the contents of this directory staying around forever.

Last, we have the Application Support directory. This is essentially used to hold everything else. This can include data files that the application needs to run, modifiable copies of resources from our application bundle, or even additional content from in-app purchases. It should not be used to store anything that more properly belongs in the Document, Caches, or Temporary folders.

It’s important to remember that your application can both read and write to the Application Support directory. If you just need to read a resource file, then you should probably load it directly from the application bundle (see the “Reading Resource Files” sidebar for more information).

On the other hand, the Application Support directory and the application bundle often work in tandem. The application checks to see if the support directory has a desired data file. If it does, the application loads the file and proceeds as normal. However, if it does not, the application copies the default data file from the application bundle and then loads it. The application can then modify the version in the Application Support directory, but the original copy in the application bundle remains untouched. This is a great way to handle user-modifiable templates and similar resources.

To be a good iOS citizen, our application should try to respect these categories and save our files in the proper locations. Of course, to do this we need either a path or a URL that points to the correct directory.

While iOS provides a number of ways to programmatically generate these paths, Apple recommends using the `NSTemporaryDirectory()` function for temporary files and either the `NSSearchPathForDirectoriesInDomains()` function or one of `NSFileManager`’s URL-based methods (`URLsForDirectory:inDomains:` or `URLForDirectory:inDomain:appropriateForURL:create:error:`) for persistent data.

## 原神

炽烈的炎之魔女

圣遗物是原神中非常重要的装备，它们能够为角色提供各种属性加成。

玩家可以通过完成副本、任务或者击败怪物来获取圣遗物。

- 理之冠
- 时之沙
- 空之杯

### HOW THE SYSTEM MANAGES DIRECTORIES (continued)

Apple currently appears to be cracking down on applications that save large files to either the Document or Application Support directories. This is especially true of any files downloaded from the Internet. As a rule of thumb, all downloaded content (at least, any significant amount of downloaded content) should be saved to the Caches file. Obviously, this could create a problem, since files in the Caches folder may be cleared whenever the device runs low on disk space.

Imagine the following situation: A user downloads a number of maps for a GPS app before hopping on an international flight. The application saves these files to the Caches folder. Next, the user downloads an audio book. This uses up most of the device’s available space, triggering a low disk space warning. In response, iOS clears all the Caches folders. When the user gets off the plane, they will discover that they no longer have the maps they needed—and without an international data plan, there’s no good way to download replacements.

Developers are currently talking with Apple about this issue, so don’t be surprised if this policy is refined as iCloud usage matures.

### FILES COPIED DURING UPDATES

When you update an application, the new application is saved to the device’s drive. Then, some files are copied from the old application to the new one. Finally, the old application is deleted.

All files within the Document folder and within `<Application_Home>/Library/` are copied during an application update. This means the Application Support and Caches directories are both copied, as are any custom directories within `<Application_Home>/Library/` (e.g., the Private Documents directory mentioned previously).

The Temporary directory is not copied.

NSTemporaryDirectory() simply returns an NSString containing the path to your application's Temporary directory. On the device, this will have the following format:

```
    /private/var/mobile/Applications/
    8BE8C8F8-D259-4E35-A515-1F5DE7E0E411/tmp/
```

On the simulator, the path points to something like the following:

```
    /var/folders/30/30GdsGkgF6mT1duyW7yCsk+++TI/-Tmp-/
```

NSSearchPathForDirectoriesInDomains(), on the other hand, takes three arguments—an NSSearchPathDirectory, an NSSearchPathDomainName, and a BOOL. It then returns an NSArray of NSString paths matching your arguments.

The NSSearchPathDirectory specifies the type of directory that you are looking for. The NSSearchPathDomainName value describes where you should look (system files, user files, etc.). The BOOL determines whether the tilde (~) in the returned paths is expanded.

In Mac OS X (and most UNIX systems), the tilde represents the current user's home directory. On iOS, it refers to the application's sandboxed directory.

Remember, these methods were originally developed for Mac OS X on the desktop, which has a much more open and much richer file system. As a result, there are a large number of legal arguments that sound intriguing but that, quite honestly, don't do anything useful on iOS.

Additionally, the desktop version often finds multiple matching directories (particularly when searching across all domains). Because of this, NSSearchPathForDirectoriesInDomains() returns an NSArray of NSStrings. In iOS, there is usually only one possible path for each directory, so we simply grab the first path (or equivalently the last path) from the list.

The bottom line is that, of all the possible domain and directory combinations, we really only use three search path directories when developing iOS applications: NSDocumentDirectory, NSCachesDirectory, and NSApplicationSupportDirectory. As you might guess, these correspond to our Document, Caches, and Application Support directories. In all three cases, NSSearchPathForDirectoriesInDomains() must use the NSUserDomainMask, as shown below:

```
    // Document Directory
    NSArray* documentPaths =
```
