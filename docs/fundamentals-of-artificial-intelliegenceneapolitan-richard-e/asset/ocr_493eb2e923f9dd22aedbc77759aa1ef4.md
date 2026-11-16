Our goal is to get this entropy down to 0 as quickly as possible so we know the value of \( Activity \). Notice that if we found out that the value of \( Outlook \) was rain we would know that the value of \( Activity \) was to stay home because we stayed home on every one of the 4 days it rained, and we would have achieved our goal. On the other hand, if we found out that the value of \( Outlook \) was sunny, the probability that the value of \( Activity \) is tennis would be 5/6 because we played tennis on 5 of the 6 days it was sunny, and we would be close to an entropy of 0. So it looks like we can possibly gain a lot of information by learning the value of \( Outlook \). To formalize this notion, we compute the expected value of the entropy of \( Activity \) conditional on \( Outlook \), which we denote as \( EH_{Outlook}(Activity) \). To obtain this value, we first compute

\( H_{rain}(Activity) = - \left( \frac{4}{4} \log_2 \frac{4}{4} + \frac{0}{4} \log_2 \frac{0}{4} + \frac{0}{4} \log_2 \frac{0}{4} \right) = 0 \)

\( H_{sunny}(Activity) = - \left( \frac{5}{6} \log_2 \frac{5}{6} + \frac{1}{6} \log_2 \frac{1}{6} + \frac{0}{6} \log_2 \frac{0}{6} \right) = .650 \)

\( H_{overcast}(Activity) = - \left( \frac{2}{4} \log_2 \frac{2}{4} + \frac{2}{4} \log_2 \frac{2}{4} + \frac{0}{4} \log_2 \frac{0}{4} \right) = 1. \)

By \( H_{rain}(Activity) \) we mean the entropy of \( Activity \) given that it rains. We then have that

\( EH_{Outlook}(Activity) = H_{rain}(Activity)P(rain) + \)
\( H_{sunny}(Activity)P(sunny) + \)
\( H_{overcast}(Activity)P(overcast) \)

\( = H_{rain}(Activity) \frac{4}{14} + \)
\( H_{sunny}(Activity) \frac{6}{14} + \)
\( H_{overcast}(Activity) \frac{4}{14} \)

\( = 0 \times \frac{4}{14} + .650 \times \frac{6}{14} + 1 \times \frac{4}{14} \)
\( = .564. \)

So we can expect to reduce the entropy of \( Activity \) from 1.531 to .564 if we learn the value of \( Outlook \). We define this difference to be the **information gain** associated with \( Outlook \). That is,

\( Gain_{Outlook}(Activity) = H(Activity) - EH_{Outlook}(Activity) \)
\( = 1.531 - .564 = .967. \)

It is left as an exercise to compute the gain associated with the other three variables, and show that \( Outlook \) has the largest gain. The ID3 Algorithm therefore makes \( Outlook \) the top node in our decision tree. For each value of