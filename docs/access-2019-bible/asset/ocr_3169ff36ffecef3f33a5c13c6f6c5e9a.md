# Validating user input

One of the most important bulletproofing techniques is to simply validate everything the user enters into the database. Capturing erroneous data input during data entry is an important safeguard that you can build into your applications. In many cases, you can use the table-level validation (determined by each field’s ValidationRule and ValidationText properties), but in many other cases you’ll want more control over the message the user receives or the actions taken by the database in response to erroneous input.

One of the major problems with the ValidationRule property is that it isn’t checked until the user actually tabs to the next control, making it impossible to capture bad data entry. You’re much better off in many cases validating entries in code. Very often you’ll want to validate all controls on a form from the form’s BeforeUpdate event instead of individually checking each and every control on the form.

# Using the /runtime option

If you’re not concerned with protecting your application and you just want to prevent users from mistakenly breaking your application by modifying or deleting objects, you can force your application to be run in Access’s runtime mode. When a database is opened in Access’s runtime mode, all the interface elements that allow changes to objects are hidden from the user. In fact, while in runtime mode, it’s impossible for a user to access the Navigation pane.

When using the runtime option, you must ensure that your application has a startup form that gives users access to any objects you want them to access. Normally, this is the main menu or main switchboard of your application.

> NOTE
> In order for the StatusBarText to be used, the status bar must be displayed (see Figure 31.1).

> TIP
> To assign a form as a startup form, open the database that you want to use, select the File tab, select Options, and select the Current Database tab. Under Application Options, set the Display Form drop-down list to the form you want to be the startup form for the application. Startup forms are covered in more depth in the "Polishing Your Application" section earlier in this chapter.

Earlier in this chapter, in the "Making the application easy to start" section, you read how to create a Windows shortcut that launches an Access application. Forcing run-time behavior in Access is quite easy. Simply add the /runtime switch after the reference to the database file in the shortcut properties, as shown in Figure 31.18.