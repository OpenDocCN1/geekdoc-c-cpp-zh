The storyboard lets you plot out exactly which elements will be moving, how fast they are moving, where they are moving, and so on.

The animations contained within a storyboard can be anything from simple animations that change one property from a source value to a target value to complex animations, such as key frame animations, where you indicate what a property’s value should be at specific time markers.

The animations I used in the preceding example are double animations, which animate a property of type double from a source value to a target value over a specific period of time.

# Migrating from Tab Bar Applications

In iOS applications, the tab bar control is an extremely common control that shows up in thousands of applications in the App Store. The purpose of this control is to segment an application into categories or provide quick, shortcut-style access to particular pieces of the application’s functionality. When there are more tabs than can be displayed on a single bar, a More button appears, which brings the user to a table view displaying the list of the remaining tabs. Tapping on any of the tabs launches the view controller associated with that particular tab.

Although Windows Phone 7 doesn’t have its own exact replica of the Tab Bar control, WP7 developers have plenty of options for building UIs that serve the same purpose as the Tab Bar control. These include the Pivot control, the Panorama control, and finally the Application Bar control. The following sections cover each of these controls respectively and how they support “tab bar-like” functionality.

# Using the Pivot Control

The Pivot control is an incredibly powerful control but also just as easy to use. A Pivot has a title and then a series of PivotItem child controls. Each of these PivotItem controls contains a XAML hierarchy of visual elements that can be anything from list boxes to buttons to whatever you like.

When the Pivot control first appears, the first pivot item is visible, and the title of the second pivot item is visible at the top of the Pivot control next to the first. Tapping the title of the second pivot item will pivot or slide the focus from the first pivot item to the second. This continues until you reach the last pivot item where the title of the first pivot item appears, allowing you to continuously move through the items without having to worry about using the back button.

One of the places you will see the Pivot control used extensively is Outlook for WP7. You can “pivot” between different views of your mail and, when used in your application, you can pivot between different categories of information or different areas of functionality within your application.