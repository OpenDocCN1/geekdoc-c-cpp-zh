
but that’s a separate philosophy altogether, something we won’t get into here.) Here are the three general ways people discover classes:

- Look at the glossary you developed during the requirements workflow, searching out the nouns and the verbs.
- Use CRC cards, which stands for Class, Responsibilities, and Collaborators (as described in “Using CRC cards,” later in this chapter).
- Look for hidden or missing classes.

We recommend doing all three; or do either of the first two along with the final one. The final item on the list is important in case you missed anything.

### Searching for nouns and verbs

As much as it sounds like a drag, searching for nouns and verbs is actually a fun process. Not all computer programmers are known for their love of human language grammar (such as English or Spanish), but you don’t have to be a grammar whiz to make it through this stage. (There are exceptions, and we tend to write books!)

First, go through the glossary and any other documents you accumulated during the requirements workflow, and begin making two lists: all the important nouns and all the important verbs.

After you have compiled your list, think about which of the nouns are particularly important; for instance, some nouns may be major aspects of the application. If you’re writing an application that models a grocery store, for example, *cash register* is probably a pretty important noun. If you’re writing an application to control an intergalactic space ship, everybody knows that the antigravity booster is vital. These, then, are good candidates for classes. You will make most of the remaining nouns characteristics in your classes. (Remember that, ultimately, characteristics and capabilities will be member variables and functions, but you’re not thinking about programming at this point.) If, however, you find a characteristic that just doesn’t seem to work with any class, you probably want to make it a class as well. Finally, the verbs will become the capabilities of the classes. You should not have any capabilities that are without a class: Either you don’t need the capability, or you are probably missing a class. Go ahead and add it.

### Using CRC cards

People love CRC (Class, Responsibilities, and Collaborators) cards because they find that creating them is fun. Big corporations like to do this type of thing during team-building exercises to help employees get along. In addition to climbing ropes and such, they design software with CRC cards.

People often use sticky notes for CRC cards, although we usually just draw them on a whiteboard. (But we’re not supposed to admit that because our fellow object-oriented people will be angry with us.)

A CRC card consists of three parts. The top part is the name of the class. The left side shows the responsibilities (what we call *capabilities*) of the class. The right side features the collaborations, which means you just list other classes that this class works together with. For example, an antigravity booster class certainly works together with a high-energy proton accelerator class, as everybody knows. You list the names of these classes on the right side of the card because they are collaborations.

![](img/6ba99460b0feb3585671a4612ff5fabb_294_0.png)

Some people prefer to put their CRC cards as sticky notes right on a whiteboard; then instead of writing the names of the related classes on the right side of the card, they just draw a line between the cards. You can either list the classes or draw lines, whichever you like best.

![](img/6ba99460b0feb3585671a4612ff5fabb_294_1.png)

By coming up with collaborations, you will spot missing classes. For example, because you know that the antigravity booster works with a high-energy proton accelerator, when you fill in the collaborations for the antigravity booster class, you will know whether you forgot about the high-energy proton accelerator class.

### Look for hidden or missing classes

It’s possible that when you do a class analysis, you will have left out some classes. Some of these missing classes may not be obvious, and to find them, you will probably have to get back with the people who helped suggest requirements. This is a good time to have them review the classes. Remember, the classes that you are building right now are not final classes ready for C++. Instead, these are less technical classes that are understandable by people who don’t program. Therefore, the people who offered the requirements and the people who will be using the application can probably look over the classes and help you determine if you are missing anything. After you determine that you have missing classes, go ahead and add them by making another CRC card.

### Completing the analysis with the design workflow

After you have your classes, you can move to the design workflow and write the classes in UML form. This is a simple form in that you will have a box with the class name at the top followed by the characteristics of the class and finally followed by the capabilities of the class. (Refer to Figure 1-3 for an example of a class in this form.) These are the classes you will use in the coding phase (*implementation workflow*), where you actually transform them into real, breathing C++ classes. The remaining chapters in this book show you how to do all this.

Book II Chapter 1 Planning and Building Objects

## Chapter 2: Describing Your Program with UML

### In This Chapter

- Moving up to UML and modeling with it
- Designing with diagrams
- Going through iterations
- Stepping through phases
- Performing workflows

The ancient people knew something that we don’t know. Instead of wasting their time writing these big, long sentences and descriptions, they used hieroglyphics, pictures that just got right to the point. One picture = one statement. It wasn’t until the twentieth century that people in the computer world started getting back to their ancient roots and realized that maybe there was something to be said for all those drawings and pictures. One day, while working late, a small group of researchers realized that a nifty way to describe software is through drawings. And thus they came up with the Unified Modeling Language, or UML for short (pronounced, well, just You-Em-El).

In this chapter, we talk about what UML is and how you can use it to model your applications. We give a brief overview of the types of diagrams it includes, and we talk about the difference between a methodology and a modeling language.

### Moving Up to UML

The Unified Modeling Language has an interesting history. When object-oriented programming was just getting off the ground in the late 1980s, several people came up with different ways to draw various diagrams to help people design their classes. This, of course, was nothing new. In addition to ancient people who used drawings in their hieroglyphics, people have always had a tendency to draw diagrams to describe something. For example, people might draw a chart listing the different parts of their applications. Or they might draw a chart that shows the steps that an application goes through, using a form called a flowchart.

A flowchart is simply a diagram that shows the step-by-step nature of a process, complete with the decision making that the process might involve. For example, we might have a step-by-step process (or *algorithm*) we use that helps us decide what to do on Mondays. This might look like Figure 2-1.

![](img/6ba99460b0feb3585671a4612ff5fabb_297_0.png)

**Figure 2-1:** A flowchart shows simple steps in a process.

In Figure 2-1, we start at the top in the spot called *Start*, and then we follow the arrow down to the first box. The first box is a command or statement — something that we *do*. Then after we do that, we follow the arrow down to the next box. After that we follow the arrow again, but this time we encounter a diamond. A diamond contains a decision. We answer the question, and if our answer is *yes*, we go one way, but if our answer is *no*, we go the other way. In this case, if it’s *yes*, we go to the right, and begin the boxes on the right, following the arrows, responding to any decisions we find. If the first decision was *no*, we follow the arrows on the left, again doing what the boxes tell us and answering any questions we see in the diamonds.

Well, this whole flowcharting business works great for small, simple tasks. But over the years, software has become far more complex. For one thing, people now build their applications around objects and classes, which simply don’t fit to the flowchart idea. And second, software has become *big*. Just a quick look at some of the software you use on a daily basis, such as the word processors, and you can see that these applications were written by lots and lots of people who seemed like they wanted to add every bell and whistle — whether you even use it or not! And the flowcharts are more suited to small portions of a software package, such as a single function or an algorithm.

And so, over the years, people have pretty much ditched the flowcharting and left it in a time capsule somewhere to be found hundreds of years from now. (Although, a portion of UML — called an *activity diagram* — is similar to a flowchart.) And during the years since programmers have started ditching flowcharts, a few well-respected researchers in the field of computer science have come up with new ways to draw pretty pictures that will describe a computer application. Several different attempts have been made, but it seems like programmers have finally come up with one that everyone can live with: UML.

UML takes the concept of flowcharting to a whole new level. Yes, that sounds like it came from a marketing brochure, but it’s true. UML is *much more* than just flowcharting. UML uses symbols that show how all the classes and objects fit together in your application, and it shows how they interact and *collaborate*. You then use UML as you design and build your entire software systems. Figure 2-2 is an example of a UML diagram.

![](img/6ba99460b0feb3585671a4612ff5fabb_298_0.png)
