# Complex Problem

Tell me about a time when you used data to solve a complex problem.

Things to Consider

+   - Did you describe how you obtained the data?
- Did you summarize the top insights from your analysis?
- What decisions did you make from the data?

Common Mistakes

+   - Choosing an example with a simplistic data set like Google Analytics or AdWords data.
- Talked about how one analyzed data but did not:
  - Share unique, remarkable interpretations or insights
  - Recommend business decisions or follow-up analyses

# Answer

CANDIDATE: During one of our mobile game launches, we had users complaining about crashes in different places of the game. At first, I asked them what kind of devices they were using, because I figured they were probably all on the same line of devices. After getting feedback from our users, I found the crashes happened across multiple devices, not just one type of device. I was stumped. Could these all be unconnected?

I asked the development team to look at each bug report. In the meantime, I went into the data. We never tested the software across every single device; we didn't have access to thousands of different mobile devices. Therefore, the scenario was new for me.

The developers got back to me. They told me they could not replicate the crashes in our lab environment, primarily because they didn't have access to the same devices. However, they did find one interesting piece of data: the users' bug reports were related. Every scenario called upon the UI element, a small window. They told me we'd probably have to get the devices in the crash reports, so they could test and debug appropriately.

I didn't want to go on a wild goose. Looking for rare mobile devices could take days, or months. In addition, it'll cost money. So I went back to the crash reports. I discovered all of the devices were Korean Samsung devices. Moreover, all the devices had Samsung Galaxy Apps.

I shared my discovery with the developers. They dug into it and saw that Samsung's Galaxy Apps interfered with the small window UI call our app was making. We found a device in the lab with Samsung's Galaxy Apps built it, and we quickly replicated the bug. And the good news: our engineers fixed the bug and rolled out an update in four hours.

To prevent this from happening again, I created a device information reference page. We use that reference page to better pinpoint problems. The reference page allows any engineer, product manager or support team member to get information about devices. It can filter by country, default apps and services.