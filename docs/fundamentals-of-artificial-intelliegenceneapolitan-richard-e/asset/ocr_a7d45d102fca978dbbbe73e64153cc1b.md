P(ELISA = positive|HIV = absent) = .002. (5.9)

You might wonder why we called these subjective probabilities when we obtained them from data. Recall that the frequentist approach says that we can never know the actual relative frequencies (objective probabilities); we can only estimate them from data. However, within the subjective approach, we can make our beliefs (subjective probabilities) equal to the fractions obtained from the data.

It might seem that Sam almost certainly is infected with HIV, as the test is so accurate. However, notice that neither the probability in Equality 5.8 nor the one in Equality 5.9 is the probability of Sam being infected with HIV. Because we know that Sam tested positive on ELISA, that probability is

P(HIV = present|ELISA = positive).

We can compute this probability using Bayes' theorem if we know P(HIV = present). Recall that Sam took the blood test simply because the state required it. He did not take it because he thought for any reason he was infected with HIV. So, the only other information we have about Sam is that he is a male in the state in which he resides. Therefore if 1 in 100,000 men in Sam's state is infected with HIV, we assign the following subjective probability:

P(HIV = present) = .00001.

We now employ Bayes' theorem to compute

P(present|positive)
= 
\frac{P(positive|present)P(present)}{P(positive|present)P(present) + P(positive|absent)P(absent)}
= 
\frac{(.999)(.00001)}{(.999)(.00001) + (.002)(.99999)}
= .00497.

Surprisingly, we are fairly confident that Sam is not infected with HIV.

A probability such as P(HIV = present) is called a prior probability because, in a particular model, it is the probability of some event prior to updating the probability of that event, within the framework of that model, using new information. Do not mistakenly think it means a probability prior to any information. A probability such as P(HIV = present|ELISA = positive) is called a posterior probability because it is the probability of an event after its prior probability has been updated, within the framework of some model, based on new information. In the previous example, the reason the posterior probability is small even though the test is fairly accurate, is that the prior probability is extremely low. The next example shows how dramatically a different prior probability can change things.