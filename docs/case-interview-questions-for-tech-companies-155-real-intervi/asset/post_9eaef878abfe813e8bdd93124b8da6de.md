
CANDIDATE: So new projects uploaded can come from existing or new users. Is there an issue with new users?

INTERVIEWER: Let's assume that there's nothing going on with new users.

CANDIDATE: Let's explore the existing user branch. The three things that can affect new projects uploaded from existing users can include:

- # of Original projects uploaded
- Upload method
- Platform

Did I miss any?

INTERVIEWER: That looks like a good list.

CANDIDATE: Let's start from the bottom first. Is there anything that indicates changes in the following:

- Number of new projects completed
- % completed projects that are uploaded

INTERVIEWER: What do you think would affect the number of new projects completed?

CANDIDATE: Seasonality. Number of new projects completed are usually are down on weekends and holiday seasons like summer.

INTERVIEWER: Good intuition, but let's say there's nothing in our research that indicates that's the issue.

CANDIDATE: Okay, let's go to the top of the list. Do we have data that indicates pins are down by device whether it's mobile or desktop?

INTERVIEWER: Weekly visits on those devices seem to be normal, but the number of new projects uploaded is down on PC and Mac.

CANDIDATE: There could be three reasons for it: OS upload dialog and drag-and-drop

INTERVIEWER: You got it. Uploads via drag-and-drop is down on both PC and Mac.

CANDIDATE: What happened?

INTERVIEWER: Nice job answering the question. We pushed out a new server-side change last week that crippled drag-and-drop upload. We just resolved the issue yesterday with a new server-side release.

## Diagnose Sales Metrics

We, the sales team, missed the $5M in new revenue target last quarter. Diagnose what happened.

### Things to Consider

- List all the factors that can affect new revenue.
- Evaluate each one.

### Common Mistakes

- Wasting time exploring existing revenue, given that the question prompt is about new revenue.

## Answer

CANDIDATE: If we missed the $5M new revenue target, that must mean:

1. We closed fewer deals than expected.
2. We closed deals at a lower average deal size.
3. Both 1 and 2 happened.

INTERVIEWER: Average deal size was not bad. In fact, it was 5% higher than expected.

CANDIDATE: Then it must be the number of closed deals.

INTERVIEWER: Correct.

CANDIDATE: Let me brainstorm reasons why number of closed deals may have gone down last quarter. I'll say by drawing out the sales funnel:

![](img/0d3703ff8680acec2ca39cc52072bee0_117_0.png)

Working backwards from closed sales, did we have issues convert sales qualified leads into closed sales?

INTERVIEWER: No, the conversion rate from sales qualified leads to closed sales was well within our expectation.

CANDIDATE: How about the conversion rate from marketing to sales qualified leads?

INTERVIEWER: That conversion ratio was within our expectation as well.

CANDIDATE: How about the conversion rate from unqualified to marketing?

INTERVIEWER: The conversion rate was down, but it doesn't explain the whole story.

CANDIDATE: Let's start with the reduced conversion rate from unqualified to marketing qualified leads. Are there any hypothesis there?

INTERVIEWER: What do you think the reasons might be?

CANDIDATE: Thinking off the top of my head, here are some reasons why marketing qualified leads went down:

- Marketing vendor did not follow up on qualified leads
- Lead quality went down, making it harder to qualify

INTERVIEWER: Why do you think lead quality might go down?

CANDIDATE: Lead quality can go down when:

1. Can't find enough high-quality prospects
2. Can find high-quality prospects, but don't have the right contact information
3. Leads may have purchased in a more favorable economic environment but not now

INTERVIEWER: Okay, these are all good ideas.

CANDIDATE: So what actually happened?

INTERVIEWER: We had a re-organization where we hired a new VP of marketing. The new VP of marketing froze our marketing budgets while she audited our existing spend. That delayed our new purchase order to the marketing vendor, so potential leads sat on the wayside until we could resume our contract.

## Chapter 14 Metrics: Putting it Together

## Fix Facebook Ad Views

Facebook ad revenue went down 10% last week. What happened? And how would you fix it?

### Things to Consider

- Start with brainstorming potential reasons, using either the AARM or E5 framework.
- Next, identify the root cause.
- Finally, make recommendations on how to address the issue.

### Common Mistakes

- Not using a metric framework, which makes it harder to brainstorm a list of potential root causes
- Not giving the interviewer a roadmap, making the answer hard to follow.

## Answer

CANDIDATE: Give me a few seconds to collect my thoughts.

INTERVIEWER: Sure.

Candidate takes seven seconds.

CANDIDATE: Here is how I want to approach the question:

1. Brainstorm a list of potential reasons
2. Identify the root cause
3. Brainstorm ways to fix
4. Make a recommendation

INTERVIEWER: That's a sound plan. Go for it.

CANDIDATE: Give me a moment to brainstorm reasons why ad revenue might be down.

Candidates takes 30 seconds.

CANDIDATE: Okay, here’s what I came up with:

| Visits | | |
| :--- | :--- | :--- |
| By Day | Per Week | |
| Traffic Source | | |
| Web: Chrome, Edge, Firefox | Mobile: Android, iOS | |
| Time on site | | |
| Impressions | Clicks | |
| Revenue per Ad | | |
| CPM / CPC | CTR | |
| Total Ad Revenue | | |

INTERVIEWER: Interesting. Walk me through it.

CANDIDATE: When it comes to total ad revenue, there are really two primary drivers: number of ads shown and the revenue per ad. If you don’t have a preference, I’ll start with the drivers that affect the number of ads shown.

INTERVIEWER: Okay.

CANDIDATE: The first thing I’d ask: have there any significant week over week changes in visits?

INTERVIEWER: No.

CANDIDATE: How about any differences in traffic type? Mix shift from web to mobile? Or mix shift from iOS?

INTERVIEWER: Why would that affect revenue?

CANDIDATE: It’s hard to type on a smartphone.

INTERVIEWER: I see that you’ve written traffic by type. Why would we care if someone using Chrome vs. Edge?

CANDIDATE: The behavior of a Chrome user is different from an Edge user. Since Chrome is usually not pre-installed by default on Windows or Mac, savvy users have to go through extra effort to download and install the Chrome browser.

INTERVIEWER: Okay. Let's say there are no differences in traffic source.

CANDIDATE: How about time on site?

INTERVIEWER: Why would time on site go down?

CANDIDATE: Sometimes time on site can go down due to seasonality. Other times on site can go down when there's a bug that prevents the user from using products effectively.

INTERVIEWER: Let's say it's none of those.

CANDIDATE: How about revenue per ad?

INTERVIEWER: Revenue per ad is definitely down.

CANDIDATE: Is it because our CPMs or CPCs are down?

INTERVIEWER: No perceptible changes there.

CANDIDATE: So then a CTR impact?

INTERVIEWER: Yes, CTRs are down.

CANDIDATE: Is there a reason why CTRs are down?

INTERVIEWER: What are some potential explanations for a decreased CTR?

CANDIDATE: Give me a few seconds to brainstorm some ideas.

Candidate takes 20 seconds.

CANDIDATE: I came with a couple of ideas on why CTR may be down:

1. Client-side suppression of ads, with the use of adblockers, can lead to reduced CTRs.
2. Ad inventory may have changed. There's a higher percentage of clicky ads than before.
3. User behavior may have changed. Users are getting smarter about not clicking ads.
4. Ad layout or placement may have changed, especially if the size of the ad changed or if the ad moved to the bottom.

INTERVIEWER: You got it. The ad inventory changed. We banned an advertiser that was promoting weight loss supplements. The ad claims were grossly inflated, and consumers complained about the advertiser's landing page experience.

CANDIDATE: Good to know.
