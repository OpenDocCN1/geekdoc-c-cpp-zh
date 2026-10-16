
only with people who already work at that hospital, you will get testers who are familiar with the hospital's processes and all the related medical jargon. However, new hires at that hospital may not be familiar with these things and may encounter usability issues that nobody in your test group did. So although it makes sense to include people from your target audience, you should never limit your testers to people from that group.

The same applies to existing users or people who have already participated in usability tests for a specific product. If you are designing an update to a product, it often makes sense to do a subset of your tests with people who have some familiarity with your product. These people may have learned specific behaviors that cause them to navigate your user interface differently from novice users. Focus on testing with people who don’t bring any preconceptions to the test but do include some tests with existing users.

When it comes to testing, one thing that can matter a lot is cultural background. Symbols and colors mean different things to people from different parts of the world. For example, Japanese video games often indicate victory by displaying a huge red ring, which kind of looks like a stop sign. Although this indicates winning to Japanese audiences, it typically conveys the opposite message for Western audiences.

If you’re expecting a lot of people with different cultural backgrounds to use your product, it makes sense to reflect this diversity with your testers.

And finally, although this book doesn’t cover accessibility,³ I will mention here that it often makes sense to do usability tests with people with poor eyesight, with older people, and generally with people who have disabilities that might affect how they can interact with your product. Doing this can help uncover accessibility issues that would have gone unnoticed.

The main point remains: don’t spend too much time trying to recruit testers from a specific demographic. Most of the time, people will find the same kinds of usability issues, regardless of their background.

3. If you’re looking for information on accessibility, check out Mark Pilgrim’s "Dive Into Accessibility" at http://diveintoaccessibility.org, and Joe Clark’s website at http://joeclark.org.

## 28.5 How to Find Testers

There are many different avenues you can use to find testers. Here are some ideas to get you started.⁴

- *Friends and relatives.* The easiest way to start recruiting testers is to ask friends and relatives. It’s OK to reuse testers, but don’t overdo it by using the same people over and over. I would advise against using workmates for testing, since they tend to have at least some level of insight into your product that normal users won’t have.
- *Professional recruiting agencies.* There are professional recruiting agencies that will help you find testers, but definitely compare costs before committing to one of them. If you use agencies, you’re a bit more likely to get people who regularly participate in such tests, which is not always what you’re looking for.
- *Through your website.* You can also look for testers through your website; the downside there is that you’re likely to get existing users of your product.
- *Through a local newspaper.* Simply putting an ad in a local newspaper often works out well. If you live near a university, they probably have a pinboard where you can advertise for testers.

Keep in mind that depending on how the testers were recruited, it might be necessary to compensate them.

## 28.6 Different Types of Tests

If you’re doing a paper prototype, you’re quite restricted in how you can run usability tests. The nature of a paper prototype pretty much dictates how you test it. Usability tests with actual running code are more forgiving, and there are different schools of thought on how they should be run. I’ll roughly group them into three different types of tests: moderated tasks tests, unmoderated tasks tests, and free-form tests.

Since the type of test determines how you prepare for it, I’ll introduce the different types of tests now and explain how to run each test later.

4. Christine Perfetti offers some additional ideas in this great video introduction to usability testing: http://uxideas.com/shows/usability_tests_nutshell/.

### Moderated Tasks Tests

In a moderated tasks test, a facilitator moderates the tests and introduces the testers to different activities or tasks. The moderator then observes the testers while they work on the tasks. The facilitator stays with the testers during the test and interacts with them.

### Unmoderated Tasks Tests

In an unmoderated tasks test, the facilitator introduces the user to the usability test and explains how everything works. The facilitator then gives the user a number of tasks on a sheet of paper and leaves the room. There is no or very little interaction between the tester and the facilitator in this type of test, which rules out any influence the facilitator might exert on the tester.

### Free-Form Tests

In a free-form test, the testers are given no tasks. Instead, the facilitator encourages the testers to explore the product on their own and do the tasks that interest them. This works best if you've recruited people who already have an interest in your product (say, you've recruited testers via your website).

In reality, you will often combine aspects of different types of tests. For example, tests often start with the facilitator encouraging the tester to explore the product and then switch to task-based tests.

## 28.7 Preparing for the Test

Depending on the type of test you're running, there are different things you need to do to prepare. In most cases, you will need a computer. Uninstall all the extraneous stuff that might interrupt the test, such as virus protection software. Install the product in a way that will allow you to easily reset the system to its default state (you don't want to confuse testers with data other users have entered into the system). Install screen-recording software and a microphone. If you decide to record the user, you also need a webcam.

It's important to be as faithful to the product as possible. For example, you wouldn't test an iPad application running in a simulator on a computer if you could avoid it. Instead, you would get an iPad for the tests and run the application on the device itself. Otherwise, you would miss important problems—such as buttons that are too small to be touched with a finger but can be clicked using a mouse.

If you're going to test software that doesn't run on a computer, you might need a camera that allows you to record the session.

If you're running a moderated test, where the facilitator stays with the user, recording the session is not strictly necessary. It can sometimes be useful, though.

### Preparing Tasks

For a task test (either unmoderated or moderated), you prepare by creating tasks for your testers. Think back to the very beginning of this book, where I talked about activities, and start with those. Focus on the most basic, most important activities of the product.

Programmers use code coverage as a measure of how much of their code is covered by a test suite. When testing user interfaces, you can't measure how much of the user interface is covered by a test quite so easily. But keep “user interface coverage” in mind as a goal. You want to design your tasks so that they touch on many different areas of your user interface.

Just like with designing tasks for paper prototypes (in Chapter 11, Paper Prototype Testing, on page 104—in fact, if you want to, you can probably reuse tasks from your paper prototype usability test), you don't want your tasks to be too prescriptive, so you should come up with a scenario that one of your users might actually experience. Describe the situation and the goal; do not describe any of the actual steps, and do not use words that are visible on-screen.

Prepare at least five tasks. For a moderated test, print each task on an individual piece of paper. Otherwise, print them all on one piece.

## 28.8 Running the Test

When running the actual test, you basically have two choices: either meet the tester in person or do a remote test. In most situations, doing remote usability tests is a lot simpler and cheaper, and it removes some of the issues that in-person tests have.

I recommend starting by doing a few in-person tests first to get a feel for how usability tests work and to get used to interacting with testers. This is a lot easier if you can sit right there next to them.
