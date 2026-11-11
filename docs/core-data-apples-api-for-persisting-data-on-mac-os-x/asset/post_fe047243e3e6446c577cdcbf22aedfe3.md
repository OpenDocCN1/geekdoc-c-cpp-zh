
In Chapter 8, *Sync Services and Core Data*, on page 140, we'll discuss ways in which we can sync the data that is in our application across multiple instances. With more and more users having more than one computer, it is ever more important to be able to keep data “in the cloud” and sync it properly across machines. By the end of this chapter, we will be able to add that functionality to our application.

In Chapter 9, *Multithreading and Core Data*, on page 162, you'll see how to maximize the use of the computing power available to us. Modern desktops and laptops have more than one CPU available to use, and if the situation demands it, it is expected that our applications will take advantage of all that processing power in a parallel manner. In this chapter, we explore the safe ways to make a Core Data application multithreaded.

In Chapter 10, *Core Data and iPhone*, on page 184, we take a side step to discuss how we can use the power and flexibility of Core Data to make our iPhone development easier. In this chapter we will also be introduced to a new controller object that does not currently exist on the Desktop.

In Chapter 11, *Recipe: Distributed Core Data*, on page 207, we explore one solution for using Core Data across a distributed environment. By combining Core Data, Bonjour, and distributed objects, we can access a Core Data repository from more than one client spread across a local network. Although I would not recommend developing the next great MMORPG with this solution, it certainly has its uses.

In Chapter 12, *Recipe: Dynamic Parameters*, on page 228, the final chapter, I share one of my secrets that I used in Simply Elegant Sales and have used several times since its original design. In this recipe, we design a document-level properties storage system similar to NSUserDefaults.

By the end of this book, we will have a superior grasp of all that Core Data can do along with many practical applications of this technology. From here we can take that knowledge to build the next generation of fantastic desktop applications.

### 1.3 Acknowledgments

When I first started working with Core Data, I enjoyed it so much that I wanted to share all the discoveries that I had made with it. I soon continued sharing discoveries with other technologies as my enjoyment of the sharing became addictive. A while back I had the pleasure of meeting a fellow developer by the name of Matt Long and helped him become more proficient with Cocoa and its related technologies. During that time, we continued to share what we were learning and teaching in the form of the blog “Cocoa Is My Girlfriend.” All of that led to this book. What started out with a simple altruistic gesture has turned into the text you are about to enjoy. Along the way I have been helped by a number of fantastic developers.

First, I would like to thank Matt Long for convincing me to share what we learned in a broader space than just one on one. I think that discussion has changed both of our lives forever.

Second, I would like to thank Tom Harrington for turning me on to Core Data in the first place. Being pointed at this technology at that particular time had a drastic positive change on my development efforts at the time.

I would also like to thank one man who tends to remain behind the scenes: Brent Simmons. A quote comes to mind when I think of Brent: “Keep away from people who try to belittle your ambitions. Small people always do that, but the really great make you feel that you, too, can become great.” —Mark Twain. Thank you, Brent, for making me feel that I, too, can become great.

Lastly, I would like to thank the reviewers of this book who have caught, corrected, and pointed out my many mistakes while writing. As every developer knows, it is nearly impossible to test your own code, and the same goes for your own writing. Without the people who read this book and tested the code while it was being written, this would be a far inferior work than the one you have in front of you. The testers and reviewers of this book have gone further than I ever expected to help make sure this work is accurate.

## Getting Started with Core Data

Instead of starting off discussing theory or reviewing the concepts behind Core Data, we will dive right into writing a Core Data application. The application we build in this chapter will be used throughout the rest of the book to explore the intricacies of Core Data.

You will be learning through doing. We will build a basic application and, in the chapters following, look back through it to understand what the pieces actually do. In this book we are writing a food recipe application that uses Core Data. The concepts within a recipe application are well known, and we will avoid spending cycles on trying to figure out the concepts of the application while also trying to grok Core Data itself.

### 2.1 Our Application

Before we start building our application, we will do a quick overview of how the UI will look and work (see Figure 2.1, on the following page).

In section 1, we will allow the user to edit information about individual recipes. Each recipe can be selected in the list and its details edited next to it.

In section 2, we will allow the user to enter the ingredients of the selected recipe. Each recipe will have its own list of ingredients that can be added, viewed, and edited here.

In section 3, we will allow the user to add a picture of the recipe for reference. This is a view-only element, and the addition of the image will be handled through the main menu.

![](img/ffa5f756dbdb501d7886468ffb761ad4_14_0.png)

Figure 2.1: Our recipe application

### 2.2 Our Application Design

In this chapter, we will start at the very beginning. You will be launching Xcode and proceeding through all the steps to create the application and bring it to a usable state. At the end of this chapter, you may be surprised that the steps to create our application are so few. This is part of the allure and strength of Cocoa development. Coupled with Core Data, it is doubly so.

In the first version of our recipe application, we will give our future users the following abilities:

- The ability to add recipes with a description, type, name, image, and number of people it serves
- The ability to add ingredients to those recipes that include a name, quantity, type, and unit of measure

This first version of our application is intentionally simple. This is useful both so that we can add features to it later and thereby explore some of the abilities of Core Data and so that we can keep the distractions to a minimum while we explore Core Data.

### 2.3 Advanced Readers

If you are already a bit familiar with Core Data and building a Core Data application, please feel free to move quickly through the rest of this chapter. In this chapter, we will walk through the construction of our project and how to build its data model. The end result will be a data model like the one shown in Figure 2.4, on page 21.

![](img/ffa5f756dbdb501d7886468ffb761ad4_15_0.png)

### 2.4 Creating Our Xcode Project

The first step is to create our Xcode project. With the recent versions of Xcode, quite a few project templates are available to us, and more than one of those is based on Core Data. If you are using Leopard, then you will want to use the Core Data Application template, and if you are using Snow Leopard, then you want to select the Cocoa Application template and ensure that the “Use Core Data for storage” checkbox is selected.

Once we select which template, we will name the project Grokking Recipes, which will also be the name of our application.¹ In your Groups & Files listing in Xcode, you will see an additional folder named Models containing the data model file (see Figure 2.2, on the following page).

The basic Core Data template gives us an application that works somewhat like Address Book. In Address Book, the user has only one data file and generally accesses that data file via one window. Our recipes application will be designed around that same pattern. We will have exactly one data file that all the user's recipes will be stored in.

Once the project is created in Xcode, it is time to start building the Core Data aspects of our application.

### 2.5 Building the Data Model

Core Data applications are like database-driven applications, and in that light, we will start with building the data structures first and then move to the user interface. The three components we are going to be working with at this point are entities, attributes, and relationships.

In our design (see Section 2.2, Our Application Design, on the previous page), we already described at least two of the data objects that we

1. Although it can be changed later.
