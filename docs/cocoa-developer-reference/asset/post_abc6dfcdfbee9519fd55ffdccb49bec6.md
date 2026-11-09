
Figure 4.4

![](img/2b293e29fc15b0797f113b85dd429b6e_101_0.png)

## Joining the Mac Developer and iPhone Developer programs

Signing up as a free developer gives you entry-level access to the Developer Program. A further level is available to developers willing to pay an annual fee. In 2010 Apple revamped its Mac Developer Program, reducing the fee to $99/year from $499 but eliminating a number of benefits. In the older program, developers were given a discount on Mac hardware and could also send applications to Apple’s Compatibility Testing labs for hardware testing. More expensive tiers offered “free” tickets to the Apple Developer Convention and further discounts.

In the new program, the chief benefits are a free copy of the current version of OS X and access to advanced beta — “seed” — versions that can be downloaded in the months before the official public launch of an update. Developers can request two technical support incidents per year, where they discuss development problems with an Apple engineer who reviews their code and offers troubleshooting advice or a workaround. Access to the Apple Developer Forums and to a selection of instructional videos is also included.

The program also controls access to the App Store. Only paid-up developers are allowed to sell apps in the store. The iPhone Program is so tightly controlled that apps built in Xcode and installed on a handset expire automatically after a few months. Developers can run a build of their code on their own devices for a limited period. When this expires, the app stops working and it must be rebuilt and reinstalled. An app can only be installed permanently by submitting it to the App Store, waiting for it to be approved, and buying it.

Currently corporate and business developers can sign up for two alternative corporate programs that cost $299/yr. Only businesses with more than 500 employees and a DUNS number — an international business identifier — are eligible. The Enterprise iPhone program allows in-house distribution and development of iPhone applications, bypassing the App Store. Because Mac development is unrestricted, there is no equivalent Enterprise Program for OS X.

## Installing Xcode

After downloading the Xcode dmg file, double-click it to open it. Installation is conventional, with few surprises. Double-click the Xcode.mpkg file in the dmg folder and follow the prompts. The SDK is designed to support multiple versions of both OS X and iPhone OS. You can select these using the dialog shown in Figure 4.6. There’s no need to support older versions of either OS, but you can install them for compatibility testing.

![](img/2b293e29fc15b0797f113b85dd429b6e_103_0.png)

> **NOTE**
>
> You can use this dialog to install an additional set of Unix command-line developer tools by checking the UNIX Development box. This feature is optional — it’s not used by Xcode and isn’t required for Cocoa development. It’s useful if you’re familiar with Unix development and want to use a traditional collection of command line compiler tools, libraries, and man pages on a Mac. The tools are installed into `<usr>`.

By default Xcode is installed in a new `Developer` directory, shown in Figure 4.7, which is placed in the root directory of your Mac’s hard disk, not in a user directory. `Developer` is best left where it is — moving it may break the installation. For quick access, it’s useful to add `Developer` to the Places list in Finder.

You can view the applications included in Xcode by opening the `Applications` folder. Xcode appears at the bottom of the list. You may want to add it to the Dock, together with Interface Builder. The other applications in this folder are used less frequently.

Figure 4.6

Older versions of both iPhone OS and OS X can be useful for compatibility testing, but most builders target the most recent OS.

![](img/2b293e29fc15b0797f113b85dd429b6e_104_0.png)

It’s an excellent idea to create a `Projects` folder. When you create a project in Xcode, it’s automatically placed inside a new folder. Most developers generate tens or even hundreds of these folders, so you’ll find it helpful to collect them into subfolders; for example, to keep trials and experiments distinct from commercial projects. A separate `Projects` folder also simplifies version control.

Figure 4.7

You can add your own Project folders (not shown here) to the contents of the Developer directory, and then divide projects further into useful subdirectories. Allow at least one folder for random experimentation.

![](img/2b293e29fc15b0797f113b85dd429b6e_105_0.png)

## Creating a New OS X Project

To create an application, double-click Xcode.app. Click the large Create a New Xcode Project button, shown in Figure 4.8.

> **CAUTION**
>
> This book was prepared with Xcode 3.2.3. A preview version of Xcode 4 was released just before the book went to press. Xcode 4 offers a faster compiler and also integrates Interface Builder, which no longer works as a separate stand-alone application. Otherwise the editing and building process for applications remains recognizably similar. For more information about Interface Builder, see Chapter 7.

Figure 4.8

The Xcode start-up screen displays a list of recent projects, if there are any. It’s a good idea to review the Getting Started with Xcode tutorial for a quick overview of some of Xcode’s features.

![](img/2b293e29fc15b0797f113b85dd429b6e_106_0.png)

Xcode displays a template window, shown in Figure 4.9. The window shows a list of file and application templates supported by Xcode. Click Application in the template pane at the left of the window. Then click Cocoa Application in the template pane at the top of the window. Click the Choose button at the bottom right.

> **NOTE**
>
> If you're using the iPhone version of Xcode, you'll see an extra division at the top left for iPhone templates. Make sure you select the Application option under Mac OS X and not under iPhone OS — unless you want to create an iPhone app. iPhone and OS X templates have a different structure.

A File Selector sheet drops down from the top of the window. Type in a name such as First in the Save As: field at the top of the sheet, as shown in Figure 4.10. Keep the name short and avoid spaces: the name is used as a prefix for some of the files in the project. Using a long name here creates unwieldy filenames in the project. The name you enter also sets the application name.

Figure 4.9

![](img/2b293e29fc15b0797f113b85dd429b6e_107_0.png)

iPhone OS offers a selection of project templates, described in Chapter 19. Cocoa applications start with a single common Cocoa Application template. The other templates are more specialized and used infrequently.

> **CAUTION**
>
> You can change the application name later if you choose to, but it’s extremely difficult to rename project files. Xcode treats the build target, the application, the project name, and the project files as separate entities, with independent names.

Figure 4.10

![](img/2b293e29fc15b0797f113b85dd429b6e_108_0.png)

You can save a new project anywhere on disk, but by default this dialog selects the Developer folder. It's efficient to create one or more project folders here rather than elsewhere on disk.

Xcode creates a new template with the name you specify and opens a new project window, shown in Figure 4.11.

> **NOTE**
>
> The project window isn't maximized when it appears. You can either resize it manually or click the green button at the top left of the window to maximize it. For monitors smaller than 26", it's easier to work with a maximized project. For larger projects, you may find it more productive to have more than one project or file window open at the same time.

Figure 4.11

![](img/2b293e29fc15b0797f113b85dd429b6e_109_0.png)

When you create a new Xcode project, it appears in a single window that is a combined editor and file selector. You can have more than one project window open at a time, either switching between them manually or tiling them on a larger monitor for fast access.

Building a project is a single-click process. There's no need to define compiler options or to change any of the default settings. Click the Build and Run button at the top of the window. Xcode compiles and runs the application, creating a floating window and a new menu bar, as shown in Figure 4.12.

> **TIP**
>
> As the application compiles, it posts status information at the bottom left of the main Xcode window. Xcode is an incremental compiler — it only compiles files that have been added to the project or have changed. Depending on the speed of your Mac, it takes 15 to 30 seconds to build and run the template application for the first time. Subsequent edits build more quickly.

Although the application seems to be independent, it's running as a subprocess within Xcode. If you quit Xcode, the application is terminated. You can run an application independently by opening the Build ▶ Debug folder within its project folder and double-clicking the `.app` file.
