
## 25.1 Do the Research

Before deciding to remove a feature, make sure you have all the data. Do you know how many of your customers use that particular feature?

The best approach is to get usage data from your customers. Add a “Send anonymous usage statistics” checkbox to your settings, and ask your users whether they would like to opt in.

Help improve BizTwit by automatically sending anonymous usage statistics.

If you can’t get hard data, you can ask your users how they use your product. Polling your users can lead to interesting results. You should make sure to give people the option of also sending in a written reply to your poll, detailing exactly how they use your product.

That’s what Mac and iOS developer Manton Reece did for his Mac app Wii Transfer.¹ As a result of the survey he ran on his users, he decided to remove a feature from his app. He wrote:²

> I eventually did remove a feature, and the survey to customers served as a nice sanity check that the feature wasn’t heavily used. The interesting part, to me, is that the feature I removed was the entire 1.0 product for Wii Transfer. Literally everything that 1.0 did is now gone.

> It’s been two weeks so far without any complaints. I like to think that it removes a distraction from the app—one less place in the app that could lead the customer down the wrong path. And hopefully it’ll eliminate a tiny part of my support load, as no one can ask me questions or have problems with that feature again!

Eventually, you should have a pretty good idea of the popularity of your features. Should the results show that a feature is particularly unpopular and therefore a good candidate for removal, you should ask yourself the following:

- If only a few of my users use this feature, is it because the feature was intentionally designed that way? Is it very important but only rarely used because of its nature?

1. See his survey results at http://www.manton.org/2009/07/wii_transfer_survey.html.

2. Read what he had to say at http://www.manton.org/2010/02/removing.html.

- Do few people use the feature because the user interface is incomprehensible, hidden, or poorly named? Would people use it more often if they knew how?

- Do people largely ignore this feature because it is simply unnecessary?

Low usage data doesn't necessarily mean you should or even can cut a feature. For example, most users of a backup application very rarely use the restore function. Obviously, that doesn't mean it's OK to cut the restore function from your backup app.

Low usage is one indicator that something might be wrong. Use the data to help you come to a conclusion, but rely on your knowledge and experience to decide which features to remove, which to replace with better solutions, and which to keep.

There's more about collecting data in Chapter 34, Collecting Usage Data, on page 287.

## 25.2 Inform Your Users

Before you yank a feature, it's always best to tell your users what you intend to do and ask for their input on your decision. It's entirely possible that you missed something when deciding which features to cut. Identify the features you intend to cut, and explain why you intend to cut them.

Don't let people vote on which features to cut (a vote doesn't tell you anything about why people voted the way they did, and if you have to override the results, you're inviting a user revolt), but do take their opinions and feedback into account. These people are the ones who actually use your product, so they might have useful insights into how your product is being used in the real world—insights that you might have missed.

## 25.3 Provide Alternatives

Only a few of your customers might use a particular feature; however, it's possible that they really rely on it. So, it's always a good idea to try to provide some kind of alternative. For example, you could contact somebody who creates a product that could replace the feature you're removing and try to negotiate a discount for your existing users.

When the people at Bohemian Coding³ wanted to remove the bitmap features from their application DrawIt, they contacted Flying Meat’s Gus Mueller.⁴ They were able to work out a deal, and every DrawIt customer got a free copy of Flying Meat’s image editor Acorn. Bohemian Coding’s Pieter Omvlee told me:

> The feedback I got was mixed. Some people were happy with the improvements I made to the vector part in the same update and said they never used the bitmap part anyway. Some complained because they only used the bitmap part, but I could point them to Acorn. Lastly, I received some complaints from people who really liked the combination of both vector and bitmap in one app. Fortunately, only very few people felt that way. In general, it all went well, and I think that’s for a big part thanks to Gus Mueller’s generous offer.

If you can’t find a similar solution, another option would be to spin the feature off into its own independent, small utility. However, this sets the expectation that you will support this utility at least at a basic level. If you aren’t ready for that responsibility, don’t pick this option.

If none of these options works for you, you can also consider keeping the old version of your product available for a time so that everybody who relies on its unique features has the opportunity to download it again and, if necessary, create a local backup copy for later use.

## 25.4 It’s Your Product

The most important point is to remember that you are responsible for your product. Your customers can switch to another product if yours doesn’t suit them anymore. You can’t. You customers don’t know how popular a feature is. You do. Your customers don’t know how much work it is to support a feature and to keep it running. You do.

You are stuck with your product, so you should make sure it remains something you want to work on and can be proud of.

3. Find them at http://www.bohemiancoding.com.
4. Flying Meat is at http://flyingmeat.com.

## Takeaway Points

- Sometimes, you have to remove features from an existing product. This is never an easy decision.
- Get usage data to find out how people use your product.
- If you’re considering removing a feature, get feedback from your users before going ahead with your decision.
- Try to provide alternatives.

## Further Reading

Mac developer Brent Simmons has written repeatedly about removing features.⁵

On his blog, product manager Jeff Lash tells you not to be afraid of removing features.⁶

![](img/4c2ca26a2dc8a63bcb4d64fdf789fcc0_219_0.png)

# Chapter 26

# Learning from Video Games

We want to make our products fun. But how? A lot of different things can be fun. For example, some people think that being scared is fun. They like riding roller coasters and visiting haunted houses. Obviously, in most cases, we can't make our product more fun by making it scarier. Instead, the kind of fun we most typically experience when we use applications and websites is the one associated with what psychology professor Mihály Csíkszentmihályi calls *flow*.

## 26.1 What's Fun?

Fortunately, there is a lot of great research on the psychology of this kind of fun, and the results are rather consistent. In his book *Flow: The Psychology of Optimal Experience* [Csi02], Mihály Csíkszentmihályi explains that people experience fun when they have a goal, a way of measuring progress toward that goal, constant feedback on their success, and skills that match the challenge, neither exceeding it nor falling short. He notes that “by far the overwhelming proportion of optimal experiences are reported to occur within sequences of activities that are goal-directed and bounded by rules—activities that require the investment of psychic energy, and that could not be done without the appropriate skills.”

Similarly, in his book *A Theory of Fun for Game Design* [Kos04], Raph Koster comes to the conclusion that people who play video games have fun when they are able to master tasks; the game presents what appear to be difficult problems that make sense to the player in the context of the game’s world. The player’s ability to solve these problems is what makes the game fun. Koster writes:
