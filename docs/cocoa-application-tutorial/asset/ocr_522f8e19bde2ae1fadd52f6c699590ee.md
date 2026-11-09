+   - The **build-version-number** property identifies an iteration of the application.

The build-version-number property is specified with the CFBundleVersion key in the Info.plist file.

The build version number is made up of a string of period-separated integers. Each integer must be equal to or greater than zero. For example, 55, 1.2, and 1.2.0.55, are all valid build version numbers.

Mac OS X uses the build version number to, for example, decide which version of an application to launch to open a file when there are multiple versions in the filesystem (as determined by their application identifiers). In such cases, Mac OS X launches the application bundle with the highest build version number. To ensure the accurate operation of this mechanism, you must adhere to one version-numbering style as you release new versions of your application. That is, if you publish your application for the first time using a multi-integer build version number, subsequent publicly available versions must use the same number of integers in their build version numbers.

> > **Note:** The application's build version number does not appear in Finder windows.

+   - The **release-version-number** property specifies the version information the Finder displays for the application. When you specify both a build version number and a release version number, the About window displays the release version number, followed by the build version number in parenthesis, as shown in Figure 7-2.

Figure 7-2    Build and release version numbers in Finder preview panes and About windows

![](bbox=[0.231, 0.501, 0.908, 0.845])