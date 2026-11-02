# 13.4 EXPERIMENTAL RESULT AND ANALYSIS

# 13.4.1 Functional Modules

The architecture to realize the individual need-based data integration and organization in organic streams is shown in Figure 13.4, which consists of five major components: data collector, user need extractor, data aggregator, data integrator, and data relation analyzer.

As shown in Figure 13.4, the data collector, which is the fundamental function module in this system, is used to collect the raw data from individuals and connect with the major database, which saves the life logs of all users. The user need extractor is employed to extract individual needs, concerns, and interests from a user's life logs to generate the heuristic stones. In addition, the data aggregator works to aggregate the data related to the extracted individual needs, while the data integrator is responsible for integrating and organizing the heuristic stones with the associative drops. Finally, the data relation analyzer analyzes the major relations among these data and further organizes them to generate the associative ripples.

# 13.4.2 Experiment Analysis

Twitter data have been utilized to conduct our experiment in order to demonstrate the feasibility of the proposed framework and method.

We obtained the Twitter data set from a list of Twitter users selected from a famous Twitter list named "twitter," as well as some of their followers. The majority of the tweets that were collected for our experiment were published in April 2013. Finally, a total of 320,000 tweets were collected. In order to illuminate our method, in this case, during the time period from April 4 to 16, the key word "Boston" was extracted as the heuristic stone using the TF-IDF method, which could indicate the interest or need within this group of users. And then those data that were related to "Boston" were aggregated to form the associative drops. An example of experiment analysis results is shown in Figure 13.5.

![](bbox=[0.28, 0.78, 0.75, 0.92])

FIGURE 13.4 Algorithm for generating organic stream. (From Zhou, X.K. et al., "Organic Streams: Data Aggregation and Integration Based on Individual Needs," Proc. the 6th IEEE International Conference on Ubi-Media Computing [U-Media2013], Aizu-Wakamatsu, Japan, Nov. 2–4, 2013.)