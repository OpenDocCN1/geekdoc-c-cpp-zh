# GPU and Cloud Computing for Music Information Retrieval ■ 97

| | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---||
| Starting time of landmarks in the database | | | | | | | | | | | |
| ● | | | | | | | | | | |
| | | ● | | | | | | | | | |
| | | | ● | | | | | | | | |
| | | | | ● | | | | | | | |
| | | | | | ● | | | | | | |
| | | | | | | ● | | | | | |
| | | | | | | | ● | | | | |
| | | | | | | | | | ● | | |
| | | | | | | | | | | ● | |
| Frame index | 0 | 10 | 20 | 30 | 40 | 50 | 60 | 70 | 80 | 90 | 100 |

| | | | | | | |
|---|---|---|---|---|---||
| Differences between the starting time of landmarks | | | | | | |
| Starting time of landmarks in query | | | | | | |
| | ● | | | | | |
| | | ● | | | |
|| | | ● | | | |
| Frame index | 0 | 10 | 20 |

FIGURE 4.17 An example of finding matched landmarks, which demonstrates that if a database song and the input query are matched, the differences between the starting times of their landmarks should be similar.

for the corresponding songs and the starting time of the landmarks in the database songs. As shown in Figure 4.17, if a database song and the input query match, the differences between the starting times of their landmarks should be similar. If the time difference is≤1 frame, it is called a matched landmark. A song with more matched landmarks will have a higher score since it is more likely to be the desired song. Once the scores of each song are obtained, we could rank the top-k likely songs and return a ranked list as the final output of the QBEE system.

Based on Ellis’s implementation [10], we developed a parallelized QBEE system over GPUs. Our initial results show that, using GPUs, the system has a response time of≤1 second when comparing a 10-second query clip against a database of about 140,000 songs. Since this is still an ongoing study with all parameters that are yet to be optimized, we will report details elsewhere. The GPU-based QBEE system is publicly available at http://mirlab.org/demo/audioFingerprinting

# 4.5 CLOUD COMPUTING FOR QBSH

Cloud computing is an existing technology that allows a user to access remote devices or execute software on demand over an array of computing servers. Based on a server-slave paradigm, it is widely used for business-oriented computation of massive amounts of data. Due to different types of demands, cloud providers offer several different service models, as shown in Figure 4.18. This section focuses on the