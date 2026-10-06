# 1.3 Resources

![](bbox=[0.117, 0.068, 0.882, 0.178])

Figure 1.3 Comparison of Q-learning and relative Q-learning algorithms for the stochastic shortest path problem of [112]. The relative Q-learning is unaffected by large discounting.

to date we offer little insight for algorithm design. For example, I don't see how today's finite-n bounds will help DeepMind create better algorithms for Go or chess. The value of asymptotic statistics is underappreciated in the RL literature. The best way to make this point is through images. Figure 1.3 is taken from [114] (many similar plots can be found in the thesis of A. Devraj [107]). Technical details regarding these plots may be found in Section 9.7.

The histograms show error for a single sample (one of many) using a particular implementation of tabular Q-learning. The integer N refers to the run length of the algorithm, and the histograms were obtained from 1000 independent experiments. The "theoretical density" is what you can obtain from asymptotic statistics for stochastic approximation. In particular, this is easily estimated on limited data. In particular, it is clear after N = 10^4 samples that we have a very good variance estimate. This can then be used to obtain confidence bounds after we run to N = 10^7 (which know how we have to run once we have a variance estimate).

Variance theory for SA is used to decide run lengths. It is also used for algorithm design: for example, to adjust variables in an algorithm so that the asymptotic variance is minimized. Zap stochastic approximation and Polyak-Ruppert averaging are examples of this approach. Outside of the bandits literature, I am not aware of work in the sample complexity literature that can offer similar value for algorithm design in reinforcement learning.

# 1.3 Resources

Many of the examples introduced in Chapters 2 and 3 are adapted from Lecture Notes on Control System Theory and Design [29]. The early chapters provide useful linear algebra background, but far more control theory than is needed to follow this.

There are many textbooks on deterministic control systems. We see [15] and Murray's two-part online survey [268] for modeling and design, and much more on linear control systems in [7, 76, 205]. Bertsekakas [45, 46] provide a great treatment of optimal control for nonlinear systems, and an introduction to RL with a perspective that is similar to this book.

Luenberger [230] is my favorite introduction to optimization, and Boyd and Vanden-berghe [73] is considered the bible, with far more depth in the domain of numerical methods. See also the monograph of Bach [19].