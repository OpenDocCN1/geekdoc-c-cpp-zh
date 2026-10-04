
## Customizing the IDE

Environment — Fonts and Colors. Quick Launch is a great tool for accessing features such as options and menu commands. For more information about Quick Launch, check out: http://ly/leljcko.

One thing I like to customize the Document Window is the tab size, which controls the number of spaces that are inserted when indenting code. To change the tab size, choose Tools > Options, and then Text Editor choose All Languages set Tabs. I usually set the Tab and Indent Size to 2 spaces, leaving the other settings in the Tab untouched. Another thing I like to customize is the number of line breaks and after HTML elements. The Options window gives you full control over: Select Text Editor HTML (Web Forms) Formatting and then click Tag Specific Options. On the list you can select a tag and then with the settings on the right you can control how it is formatted. The Preview box makes it easy to see how the various settings change the formatting. Note that Web Forms has its own category in the Options dialog because it uses a different HTML editor under the hood than the HTML-based editors found in Visual Studio

If you prefer to select lines in the gutter of the Document Window, choose Tools > Options set All Languages and select the Lines checkbox.

With the exception of the Tab Size being set to 2 and the number of line breaks around a few HTML elements, all screen shots in this book show the default setup of VSEW.

## Customizing Toolbars

You can customize toolbars in three ways: you can show or hide the built-in toolbars, you can add and remove buttons from existing toolbars, and you can create your own toolbars with buttons that you use.

## Enabling and Disabling Toolbars

You disable and enable existing toolbars by right-clicking any existing toolbar or the menu bar and then selecting the appropriate item from the list. Once the toolbar is displayed, you can use its drag grip at its left to drag it to a new location in the Toolbar area.

## Editing Toolbars

If you feel that an existing toolbar is missing an important button or it contains buttons you rarely use, you can customize the buttons on it. To do this, right-click any toolbar or the menu bar, switch to the Commands tab, and select the toolbar you want to modify from the Toolbar drop-down. With the command buttons at the right, you can add new and remove existing commands, or change their order.

## Creating Your Own Toolbars

Creating your own toolbar is useful if you want to group some functions you frequently use. To create a new toolbar, open the Customize window as explained in the preceding section. Click the New button and type a name for the toolbar. Then switch to the Commands tab and modify your toolbar as you would with existing toolbars.

## Customizing Keyboard Shortcuts

Another setting many developers to change keyboard shortcuts. Keyboard shortcuts are a great way to save time because they enable you to perform a task with a simple keyboard command instead of reaching for the mouse and selecting the appropriate item from the menu. To change the keyboard shortcuts, choose Tools > Options, Expand Environment, and click Keyboard. Alternatively, press Ctrl+Q, type keyboard and hit enter. Locate the command for which you want to change the shortcut in the list of commands. Because this list contains many items, you can filter the list by typing a few letters from the command. For example, typing print in the Commands Finding filter gives you a list of all print-related commands.

Next, in the Press Shortcut Keys field, type a new shortcut and Assign. Visual Studio enables you to enter a double shortcut for a single command. For example, you can bind the Close All Documents to the command Ctrl+K, Ctrl+O. To perform this command, you need to press both combinations in rapid succession. Although a double shortcut may seem like overkill, it greatly increases the number of available shortcut keys.

## Resetting Your Changes

Don't worry if you have messed by trying out the numerous customization options. You have many ways to restore Visual Studio to its previous state.

## Resetting the Window Layout

The command Reset Window Layout, accessible from the Window menu, resets all windows to the position they were in when you first started Visual Studio. This command is useful if you misplaced too many windows and ended up with a cluttered IDE.

## Resetting the Toolbox

If you removed an item from the Toolbox by mistake or ever deleted an entire tab, you can reset the Toolbox to its original state by right-clicking the Toolbox and choosing Reset Toolbox. You need to think twice before using this command as it also deletes all your custom snippets.

## Resetting All Settings

If you followed along with the previous Try It Out exercises, and then started experimenting with the customization possibilities, your IDE is now probably in one of two states: it works exactly the way you want it, or it looks like a complete mess. In the latter case, it's good to know that it is easy to clean up the chaos.

To completely revert all Visual Studio settings to the way they were right after installation, choose Tools > Settings > Import and Export Tools > Import and Export Settings, depending on the version of VS you're using. Then choose the Reset All Settings option and click Next. If you want, you can create a backup of the existing settings; otherwise, choose No. Get another screen that allows you to choose any of settings collections. Choose Expert Settings or Web Development because these options give you access to all the features you need to follow along with this book. Finally, click Finish. This action causes all settings to be reset to their defaults, including the window layout, Toolbox and Toolbox customizations, shortcut keys, and everything you may have changed in the Visual Studio Options dialog box. So, use this command only when you're really sure you want a fresh, new set of Visual Studio.

With basic knowledge about ASP.NET pages and Visual Studio, it's time for some real action. In the next chapter, we see how to create ASP.NET websites and web pages in much more detail. You learn how to organize your site in a logical and structured way, how to add the many different types of files to your site and how to use them, and how to connect pages in your site.

However, before you proceed to the next chapter, there is one more important topic you need to look at: the sample application that comes with this book.

## The Sample Application

Building websites is what this book is all about, so it makes a whole lot of sense that this book comes with a complete and functional sample site that is to showcase many of the capabilities of ASP.NET.

The sample site you build in this book is called Planet Wrox, a site that serves as an online community for people interested in music. The site offers the following features to its visitors:

- Albums and concerts that have been posted on the site by the administrator.
- The Gig Pics section, an online photo album where users can share pictures at concerts.
- The ability to switch between the different graphical themes that the site offers, giving you a chance to change the look and feel of the site without altering the content.
- The ability to store musical preferences that influence the information users on the site.
- Access to bonus features for registered users.

The site enables that (that is, you, the owner of the site) to do the following:

- Add and maintain the reviews.
- Manage the different musical genres in the system.
- Manage photo albums created by visitors to the site.

Figure 1-16 shows another page from Planet Wrox, but with a different theme applied. This page enables users to enter their personal information and specify preferences with regard to their favorite genres.

You can find an online running example of the site at PlanetWrox.com. There you can play around the site from an end user's perspective.

You can also download the source for the sample application and all other examples from this book from the Planet Wrox site at www.wrox.com/go/begaspnet451.

By the end of this book, you'll be able to build all of the functionality from the site (and hopefully even more) in other websites. Don't worry if it sounds like an awful lot of complex things. I guide you, step by step, from the beginning of the application all the way to the last feature. As long as you keep having this thing, I'm sure you'll make it all the way.
