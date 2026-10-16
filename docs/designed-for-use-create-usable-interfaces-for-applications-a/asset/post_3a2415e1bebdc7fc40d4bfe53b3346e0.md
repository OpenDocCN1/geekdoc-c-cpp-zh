
the crafts, and finally reached into design." He lamented that many designers no longer have the good of the consumer in mind.

Making your product fun is a great goal, but fun can and should never come at the expense of usability.

## Takeaway Points

- Merely being usable doesn’t make your product fun. However, if your product isn’t usable, it’s probably not fun either.
- People experience fun if they have a meaningful challenge, a way of measuring their progress toward mastering that challenge, and the skills to master the challenge.
- Don’t provide the challenge. Your users will do that for you.
- You don’t need to set the difficulty. Your users will pick a challenge that is suitably difficult for them.
- Providing feedback on people’s progress, and allowing them to grow along with the challenges they master, makes their experience more fun.
- Try to find a way to reward exploration and positive behavior.

## Further Reading

Both *Flow: The Psychology of Optimal Experience* [Csi02] by Mihály Csikszentmihályi and *A Theory of Fun for Game Design* [Kos04] by Raph Koster provide useful insight into what makes things fun. *Rules of Play: Game Design Fundamentals* [SZ03] by Katie Salen and Eric Zimmerman is also worth reading, as is Thomas W. Malone’s paper “Heuristics for Designing Enjoyable User Interfaces,”¹³

Replica Island developer Chris Pruett writes a great blog about game design that sometimes touches on usability issues.¹⁴

On YouTube, there’s an interesting presentation called “Putting the Fun in Functional: Applying Game Mechanics to Functional Software” by Shufflebrain CEO Amy Jo Kim.¹⁵

13. You can find it at http://portal.acm.org/citation.cfm?id=801756.
14. At http://replicaisland.blogspot.com.
15. Watch it at http://www.youtube.com/watch?v=ihUt-163gZl.

## Part III

## Implementation

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_234_0.png)

## Chapter 27

## Guerilla Usability Testing

|  |  |  |
|---|---|---|
| Research | Design | Implementation |

### What’s the Technique?

Usability testing typically involves inviting people to come to you. This creates a number of issues with scheduling, setting up simple test labs, and finding people who are willing to help you out as testers. You can circumvent these problems by doing one simple thing: going to people instead of having them come to you.

### Why Is This a Good Idea?

You can do the best job possible planning and designing your product, but until you test it with real people, you don’t know how well it works.¹ By going out and asking people to do simple tasks with our product, you can quickly identify areas where your design needs additional work and fix these areas while the code is still easy to change. If you don’t invest time in finding out where your product’s problems are now, you’ll find out about them after you’ve launched it.

### Why “Guerilla”?

Ostensibly, it’s called *guerilla usability testing* because, analogous to guerilla warfare, it circumvents many of the tools and techniques of traditional usability testing in favor of a simpler, less people-intensive approach that relies heavily on mobility and on the element of surprise. However, I think, it’s mainly called guerilla usability testing because we programmers and designers like to make our jobs sound much more badass than they really are. Hi there, Code Ninjas and Rock-Star Designers!

### Are There Any Prerequisites?

Yes. You need to have running code, and at least part of your user interface needs to be working. You also need to be able to run your product on a portable device, such as a notebook, cell phone, or iPad.

### Guerilla Style

In a typical usability test, you invite people to come to you. You sit them down in front of a specially prepared workspace and ask them to do specific tasks while you record their actions. You then use the information gleaned from this interaction to improve your user interface.

This kind of testing involves quite a bit of preparation. You need to set up a workspace and devise a way of recording your testers; you need to find testers, schedule them, and maybe also pay them for their participation.

As usability testing became more widespread in the software community, people developed a set of techniques that circumvent all the process issues. This is commonly known as *guerilla usability testing*.

The main difference to a regular usability test is that we go to testers, instead of having them come to us.

### 27.1 How Often to Test

Guerilla testing is simple, requires almost no preparation, and can be done pretty much at any time. As a result, it’s often a good idea to do guerilla testing when you actually have a question you need answered.

Say you’ve come up with a new way of letting people send messages in your Twitter app. You’ve implemented it, and it works. But will people get it? Don’t guess. Instead, test.

### 27.2 Preparing for the Test

You should have your code running on a portable device. If your product relies on a service or is a service, prepare a guest login so people don’t have to supply their email addresses or other personal data. If your code relies on an Internet connection, make sure this works where you’re going. Check that your portable device’s battery is full (keep a spare if possible and necessary).

You should also think about how to explain your product and come up with some simple tasks you want people to perform. Then, make sure your product is bug-free for these specific tasks; run through each task to see whether it works. Your aim is to find issues with the user interface, not bugs in your code.

If you want to, you can install something like Silverback or Jing² on the computer to record the user’s actions.

### 27.3 How Do You Find Testers?

Simply visit a nearby café, look for people who don’t appear to be buried in the newspaper or a laptop, and ask them whether they are interested in participating in a short usability test.

If you’re working in an office building, it’s often also possible to find people near the watercooler or people who are on a cigarette break. Unless you specifically want to find out how well a new feature works for existing users, you should try to avoid people who are overly familiar with your product, though.

### 27.4 How Many Testers

Since you don’t have to schedule testers in a guerilla-style usability test, you can test with as many people as you need to until you feel you have a solid answer to your question. Three to five people is usually

2. Find these products at http://silverbackapp.com and http://www.techsmith.com.

a good idea, but even a single tester often yields useful insights into potential issues with your design.

### 27.5 Running the Test

This is pretty simple. Find somebody willing to lend you five minutes. Explain what exactly you are doing, what the application does, and what the task is that you want the person to perform. If you intend to record the session, get the user’s permission.

We’re working on a new Twitter app. You know what Twitter is? OK, great. We’re working on this app, and in order to make sure that we got the design right, we want to see whether people can figure out how to use it, so we’re testing our design. We’re not testing you. Don’t worry if you don’t immediately get something, because that’s exactly the kind of feedback we’re looking for. It means we got something wrong with our design. If it’s OK with you, we’ll record this test so that we can go through it later. We won’t publish the recording or anything like that. OK? Great. For the first test, we want to test our “new message” user interface. We’re already logged in, and we just want to see whether people can figure out how to post Twitter messages. Feel free to talk during the test and explain what’s going through your mind while you’re using the app.

Then, sit back, observe, and take notes.

It’s very likely that the tester will run into issues rather quickly. If you feel that he gets frustrated, intervene and either give a hint or stop the test. Otherwise, just keep your mouth shut.

I will talk more about how to run usability tests in later chapters, but for now, this is really all you need to know.

### 27.6 The Results

Once you’ve done this with a few people, you’ll end up with a list of problems. Some of them will likely have occurred with more than just one person, and those are the ones you want to focus on first. Think about why people didn’t get your design. Think about how to fix it. Implement a fix. Test again, until people get it.
