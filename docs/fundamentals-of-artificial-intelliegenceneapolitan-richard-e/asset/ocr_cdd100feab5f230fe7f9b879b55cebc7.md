| Edge | Causal Relationship |
|---|---|
| \( X - Y \) | \( X \) causes \( Y \) or (exclusive) \( Y \) causes \( X \); or \( X \) and \( Y \) have a hidden common cause. |
| \( X \rightarrow Y \) | \( X \) causes \( Y \) or \( X \) and \( Y \) have a hidden common cause; and \( Y \) does not cause \( X \). |
| \( X \dashrightarrow Y \) | \( X \) causes \( Y \). |
| \( X \leftrightarrow Y \) | \( X \) and \( Y \) have a hidden common cause. |

In the above, when we do not denote an “or” as exclusive, it is not exclusive. There is one additional restriction. If we have the chain \( X - Y - Z \), we cannot have two causal edges with their heads at node \( Y \). For example, we could not have node \( X \) causing node \( Y \) and nodes \( Y \) and \( Z \) having a hidden common cause.

The example now follows. Using the database collected by the U.S. News and World Report magazine for the purpose of college ranking, Drudzdel and Glymour [1999] analyzed the influences that affect university student retention rate. By “student retention rate” we mean the percent of entering freshmen who end up graduating from the university at which they initially matriculate. Low student retention rate is a major concern at many American universities, as the mean retention rate over all American universities is only 55%.

The database provided by the U.S. News and World Report magazine contains records for 204 U.S. universities and colleges identified as major research institutions. Each record consists of over 100 variables. The data were collected separately for the years 1992 and 1993. Drudzdel and Glymour [1999] selected the following eight variables as being most relevant to their study:

| Variable | What the Variable Represents |
|---|---|
| grad | Fraction of entering students who graduate from the institution |
| rejr | Fraction of applicants who are not offered admission |
| tstsc | Average standardized score of incoming students |
| tp10 | Fraction of incoming students in the top 10% in high school |
| acpt | Fraction of students who accept the institution's admission offer |
| spnd | Average educational and general expenses per student |
| sfrat | Student/faculty ratio |
| salar | Average faculty salary |

Drudzdel and Glymour [1999] used Tetrad II [Scheines et al., 1994] to learn causal influences from the data. Tetrad II allows the user to specify a temporal ordering of the variables. If variable \( Y \) precedes \( X \) in this order, the algorithm assumes there can be no path from \( X \) to \( Y \) in any DAG in which the probability distribution of the variables is embedded faithfully. It is called a temporal ordering because in applications to causality if \( Y \) precedes \( X \) in time, we would assume \( X \) could not cause \( Y \). Drudzdel and Glymour [1999] specified the following temporal ordering for the variables in this study: