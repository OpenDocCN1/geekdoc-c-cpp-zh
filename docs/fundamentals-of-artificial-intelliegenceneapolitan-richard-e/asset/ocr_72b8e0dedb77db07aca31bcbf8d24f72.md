![](bbox=[0.166, 0.083, 0.866, 0.323])

Figure 8.10 A decision tree representing Amit's decision concerning being treated for streptococcal infection.

U(suit goes to cleaners)
\equiv EU(L_q)
= qU(suit not ruined) + (1 - q)U(suit not ruined, inconvenience)
= q(1) + (1 - q)(.8) = .8 + .2q.

Let's say Leonardo decides q = .6. Then

U(suit goes to cleaners) = .8 + (.2)(.6) = .92.

Next, we give an example from the medical domain.$^1$

**Example 8.7** Amit, a 15-year-old high school student, has been definitively diagnosed with streptococcal infection, and he is considering having a treatment that is known to reduce the number of days with a sore throat from 4 to 3. He learns, however, that the treatment has a .000003 probability of causing death due to anaphylaxis. Should he have the treatment?

You may argue that, if he may die from the treatment, he certainly should not have it. However, the probability of dying is extremely small, and we daily accept small risks of dying in order to obtain something of value to us. For example, many people take a small risk of dying in a car accident in order to arrive at work. We see then that we cannot discount the treatment based solely on that risk. So what should Amit do? Next, we apply decision analysis to recommend a decision to him. Figure 8.10 shows a decision tree representing Amit's decision. To solve this problem instance, we need to quantify the outcomes in that tree. We can do this using **quality adjusted life expectancies**

$^1$This example is based on an example in [Nease and Owens, 1997]. Although the information is not fictitious, some of it is controversial.