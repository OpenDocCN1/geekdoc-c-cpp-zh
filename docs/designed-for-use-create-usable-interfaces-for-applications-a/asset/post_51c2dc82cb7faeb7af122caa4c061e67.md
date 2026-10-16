
Second, it needs to be uploaded. You could add some short explanatory text or even a little animation representing the active task near the progress bar, giving the user some indication of what is currently going on. Telling the user which stage the application is in provides an explanation for why the whole process is taking so long and can help make him comfortable with the idea of having to wait.

If a task takes a long time, it’s likely that people will focus on something else. Eventually, they may forget that the task is running at all. You can use audio feedback to indicate that the task is done; that way, people will know even if they’re paying attention to something else.

## 23.3 Perceived Speed

Speed is perception. People are not going to measure your product’s response time with stopwatches. What really counts isn’t how long an action takes in seconds and milliseconds but how your users perceive your product’s speed.

One thing you can do to improve speed perception is to start showing partial results as soon as possible. If you are implementing a user interface for a search system, don’t wait for the search to finish before you show the results to the user. Instead, start showing search results as soon as you start finding them.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_200_0.png)

Another way of improving speed perception is to make sure that actions that take a long time don’t block your product’s user interface. If your users can do something else instead of being forced to wait for a process to finish, they are less likely to notice how long the process takes.

Here's a final idea. Adding simple ripple effects that move counter to the direction of a progress bar can make the progress bar appear to move faster.³

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_201_0.png)

## 23.4 Slowing Down

Slow products are annoying, but the opposite can also be true. Sometimes, things can be too fast. A typical example of this is scrolling. If your application scrolls too quickly, users overshoot their target. It often makes sense to artificially slow down your product so people can keep up with it.

A similar problem once occurred to me when I was working on Appway, a business process management system. Its process editor includes a Save feature that allows users to manually save changes to a process. When people used the editor and wanted to save their changes, they often repeatedly clicked the Save button rather than just clicking once and sometimes complained that it did not work properly.

It turned out that the application was simply too fast for them. Saving the workflow took only a fraction of a second. The absence of a progress indicator meant users had no obvious feedback indicating that the document had actually been saved, but saving a document felt so important to them that they expected to see something reasonably substantial happen when they clicked the button. The solution was to throw up a “fake” progress indicator that took about half a second to finish.

3. As shown here: http://www.newscientist.com/blogs/nsfv/2010/12/best-videos-of-2010-progress-bar-illusion.html.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_202_0.png)

This reassured users that something substantial had happened. User experience consultant Harry Brignull refers to a similar story⁴ about coin-counting machines. Supposedly, the machines counted coins so quickly that customers did not trust that they could have counted them correctly. To fix this user experience problem, the manufacturer changed the machines to display the results more slowly and added speakers to produce coin-counting sounds while the machines waited for the counter to get to the final amount. As a result, people felt that the machine put the proper effort into counting their money and trusted the result.

## Takeaway Points

- Responsiveness and speed are extremely important properties of your products. Usability tests don’t always reveal these kinds of problems.
- To be perceived as instant, actions should take less than 0.1s.
- Actions taking more than a second should show some kind of indicator that the application is working. This should appear where the user’s focus is.
- Perceived speed is more important than actual speed. Sometimes, tricks can help you make your product *feel* faster.
- It’s possible for things to happen *too* fast. In some cases, artificially limiting the speed of some features of your product can improve the user experience.

4. View the article at http://www.90percentofeverything.com/2010/12/16/adding-delays-to-increase-perceived-value-does-it-work/.

## Further Reading

Jakob Nielsen’s essay on response time is an invaluable source of information on this topic.⁵

Bruce Tognazzini talks about latency in his list “First Principles of Interaction Design.”⁶

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_204_0.png)

## Chapter 24

## Avoiding Features

Product design is a never-ending race. To avoid being overtaken by competitors, you need to keep running and running—or, in our case, designing and designing. But this race has no clear finish line; your product is never really “done.” At most, it simply becomes a bit less unfinished with each new release. This is the best we can hope for.

Like a species of shark that needs to keep moving in order to supply its gills with oxygenated water, if your product remains stagnant for too long, it dies. This is a problem, because it means you must constantly add new things. As a result, most products are forever acquiring new features, without much thought going into it.

As you add new features, your product can quickly grow from its original state—an elegant solution to a well-defined problem—into a byzantine mess of unrelated functions. It may be that, on the whole, the product solves a number of problems, but chances are that it solves most of them poorly. The fact that a product could (in theory) solve many problems is meaningless if its users have trouble figuring out how to find the features that solve their particular problem.

Although those users with existing knowledge of your product may be able to keep up with all of the features, you are essentially closing the door for new users who do not have the benefit of starting out with a simple product and learning how to use all of the additional features as they appear.

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_205_0.png)

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_205_1.png)

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_205_2.png)

1984

1988

2010

What’s worse, your existing users, who grow alongside your product, will turn into advanced users, which means they will continue to push you to add more advanced features. If you do this, your customer base will skew even more toward advanced users.¹ It’s a vicious cycle.

How do you manage product growth and avoid adding countless new features?

## 24.1 Remember the User’s Goals

Think about what your users want to achieve with your product. Does the new feature help them produce better results? Does it allow them to reach new goals? Does it make the product easier to use? As Kathy Sierra puts it,² “People are not into your tool, they are into what the tool enables.”

## 24.2 The Five Whys

When receiving user feedback, your first task is to find out what exactly the user is trying to achieve. Often, the solution to the user’s problem can be found without adding new functionality to your product.

One process you can use to find the root cause of a problem is “The Five Whys.” According to legend, this approach was originally developed by Sakichi Toyoda, the founder of Toyota Industries. It works pretty well when trying to find out what caused somebody to send in a particular feature request: you simply keep asking “why?” (or something along those lines that sounds a little less unfriendly) until you figure out

1. Chris Clark mentions this problem at http://releasecandidateone.com/236:crotchety_old_power_users.

2. You can read more of her writing at http://headrush.typepad.com.
