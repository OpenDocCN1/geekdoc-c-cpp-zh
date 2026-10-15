
There is another kind of analysis that produces metrics summarizing your code. This type of analysis digs through your compiled code and computes statistics such as a “maintainability index” based on other values such as “cyclomatic complexity,” “depth of inheritance,” “class coupling,” and even the number of lines of code.

Cyclomatic complexity (also called conditional complexity) is a metric used to indicate the complexity of a software program. It measures the number of independent paths through a particular block of source code. A cyclomatic complexity value of 1 indicates that there is only one way to get from the beginning to the end of a block of code. If you introduce an if/else block into code that had a cyclomatic complexity of 1, it will then change to 2, indicating that you can finish that block by either going through the if section or going through the else section. The greater an application’s cyclomatic complexity, the harder it is to write unit tests for, and the larger the number of manual tests a developer must do to exercise all the code. This complexity grows naturally as an application grows, but you should keep an eye on it and possibly find ways to reduce this complexity by providing a more linear path through your code. Figure 20.3 shows some sample output from a static analysis run.

![](img/04a00d46bb1059867d95707babd62ee7_299_0.png)

Figure 20.3 Generated code analysis metrics.

Depth of inheritance, as its name implies, refers to the depth of a class within an inheritance hierarchy. The static analysis tool scores the classes in your application with a value indicating the inheritance depth. In general, the deeper a class is within an inheritance hierarchy, the more difficult it is to predict the behavior of that class and the more complex the design. Some of this you need to take with a grain of salt because control hierarchies are often deep before you even start writing your own custom control. However, if you have a view model class with a depth of 8, you might want to consider refactoring to flatten your inheritance tree a little. Figure 20.3 shows the output of the code metrics window, including the depth of inheritance rank, cyclomatic complexity score, and class coupling value.

Class coupling refers to the number of classes on which another class depends. Suppose I’ve built a class and it has two properties, and each of these properties is a different class. This one class now has a class coupling value of 2 (the static analysis tool ignores built-in .NET types when determining this metric). The general consensus is that the higher the class coupling value for a class, the less stable that class is. In other words, classes with a high class coupling value are far more likely to break after a code change than classes with a low class coupling value. MVVM, as you saw in that chapter, is designed specifically to allow you to build powerful user interfaces with a minimum of class coupling. Another tip to keep in mind is that if you convert a class-typed property into an interface-typed property (allowing for easy mocking or dependency injection via tools such as Unity or Castle Windsor), this will reduce the class coupling metric.

### Summary

Before we get into the nuts and bolts of submitting your application to the Marketplace in the next chapter, I wanted to make sure that I introduced you to some of the tools available to Windows Phone 7 developers for debugging, tracing, troubleshooting, and even analyzing code for areas of improvement.

One unfortunate fact of the software development life cycle is that no matter how quickly you manage to complete the main functionality of your application, it is going to take a very long time to hone, refine, tweak, and refactor your application after that point. Knowing how to use static analysis tools, debuggers, breakpoints, and the other techniques presented in this chapter will help take your application from a good app to a rock-solid, stable, reliable application that is more likely to pass the certification process.

Just remember that the purpose of debugging isn’t to execute without errors; it’s to find errors so that you can fix them. Try to break your application as many ways as you can and use the techniques in this chapter and in previous chapters to find and fix those bugs. Then you’ll be ready to submit your application to the Marketplace and hopefully make truckloads of money.

## Deploying Applications to the Marketplace

> The safe way to double your money is to fold it over once and put it in your pocket.
> Frank Hubbard

This chapter is all about deploying your applications to the Marketplace. You’ve written the code for your application and you’re proud of what you’ve created. You have a good application icon, a tile icon, and you’ve mastered the techniques of concern separation (possibly with MVVM). You’ve tested your application with unit testing, and you’ve debugged it and performed static analysis on the application. You’ve given the code to your friends or colleagues and gotten them to run the application—and they love it. You’re ready to submit your app to the store and start making giant piles of money.

In this chapter you’ll see a hands-on walkthrough of taking an application from the point where you’re satisfied that it’s fast, stable, reliable, and complies with all the certification requirements to the point where it’s been uploaded to the Marketplace and you can start collecting your money.

To do this, I’ll introduce you to a sample application that I wrote called Zombie Apocalypse Trainer that, interestingly enough, falls into the Health and Fitness category of the Marketplace. I will show you, step-by-step, how I took this application and went through the entire deployment and certification process, including deploying it to a test device to make sure everything worked properly.

### Introducing Zombie Apocalypse Trainer

Zombie Apocalypse Trainer is a new twist on the standard calorie-tracker application. Rather than motivating people to lose weight and keep tabs on their calories by shaming them with a log of their eating habits, this application gives people new motivation: avoiding death at the hands of hordes of brain-sucking undead.

The application asks you to set a target weight and a date by which you’d like to reach that weight. This is essentially the Zombie Apocalypse—make-it-or-break-it time. If you don’t reach your target weight by the target date, the application assumes that you are simply too overweight to avoid capture and you are going to die a slow, painful death by having your brains eaten by zombies.

Here is the description of the application that I intend to use in the Marketplace:
Are you ready for the Zombie Apocalypse? When the streets are filled with rabid, brain-eating undead, will you be able to outrun them? Use this application to track your calories burned, calories eaten, and weight log. Just tell the app when you think the Zombie Apocalypse will be and start tracking your progress.

From a technical standpoint, Apocalypse Trainer is a standard Silverlight WP7 application that was built with the use of the MVVM Light framework discussed earlier in the book. I tested the application using the unit testing techniques I discussed in earlier chapters. It has three core view models: Main, Today, and History.

The Main view model contains all the information required to supply the home screen with its useful information, such as the number of days remaining until the apocalypse and how long you have gone without being mauled (without exceeding your calorie budget).

The Today view model contains the list of food items you’ve consumed today and the list of exercises that you’ve done today. This differs from the underlying persistence medium, which contains a list of all food and exercise since you installed the application. Remember that view models are specifically designed to support the UI in its effort to render what the user wants to see, not necessarily what the data looks like on disk (or in a database or on a web service, and so on).

The History view model contains the weight log—the history of weigh-ins since you’ve installed the application. As you navigate through the application, dialogs appear that allow you to create new data. These are WP7 pages that are bound to individual view models using a view model locator (again, this is all stuff we discussed in the MVVM chapter). When the user taps the Confirm button on a dialog to create a new piece of information, a message is sent using MVVM Light’s messaging framework. The view model that holds the collection of items to which the new item will be added has subscribed to this message and, in response to the message, adds the appropriate item to the collection.

Whenever data in the view model changes, the view model asks a subordinate data service to make the changes permanent. In the case of Zombie Apocalypse Trainer, the persistence medium is isolated storage. I use the IsoStoreHelper class that was used several times throughout the book to read and write object graphs in and out of isolated storage.
