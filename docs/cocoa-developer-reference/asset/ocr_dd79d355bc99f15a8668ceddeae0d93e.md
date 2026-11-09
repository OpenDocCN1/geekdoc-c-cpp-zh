| Error type | Description |
|---|---|
| Forgotten links or bindings in Interface Builder | When you add new features to a view, don’t forget to link their outlets and actions in Interface Builder to add bindings—and don’t forget to save the nib file after editing. |
| Missing delegate features | If a class feature isn’t working, check for and implement any compulsory delegate methods. |
| Missing focus or First Responder status | Some AppKit classes may not work without window focus or First Responder status. Check that you’re handling these features correctly. |
| Broken or misaligned Xcode links | If you import files to a project or add assets to it, remember to set the Path Type to `Relative to Enclosing Group`. If you leave it set to `Default`, you may find yourself editing files across a mix of project folders. Xcode doesn’t warn you when you do this. |

![](bbox=[0.103, 0.414, 0.172, 0.47])

# TIP

Simple mistakes can waste time, but don’t let them sap your confidence or raise your stress levels. Even experienced developers regularly make basic errors.

# Managing classes and files

Xcode doesn’t include automated support to help you manage classes, properties, and files. Managing them manually makes them error prone. Use these checklists to avoid the most common errors. The steps may seem obvious, but it’s easy to miss them when you’re concentrating on some other aspect of a project.

# Including other classes in a class header

+   - Add `#import` directives for other classes that are referenced.
+   - Add `@class` directives for each class.
+   - Add `#import` directives for framework headers, as needed.

# Creating a new subclass

+   - After you create the file, change the subclass name in the interface.
+   - Add any delegate protocols, as needed.