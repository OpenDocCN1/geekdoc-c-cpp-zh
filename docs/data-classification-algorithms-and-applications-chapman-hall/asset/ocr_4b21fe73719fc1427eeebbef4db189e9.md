# 19.2 Bayesian Methods

In this section, we introduce Bayes optimal classification and its implementation approaches including Bayesian model averaging and Bayesian model combination.

# 19.2.1 Bayes Optimal Classifier

Ensemble methods try to combine different models into one model in which each base model is assigned a weight based on its contribution to the classification task. As we discussed in the Introduction, two important questions in ensemble learning are: Which models should be considered and how to choose them from the hypothesis space? How to assign the weight to each model? One natural solution is to consider all the possible hypotheses in the hypothesis space and infer model weights from training data. This is the basic principle adopted by the Bayes optimal classifier.

Specifically, given a set of training data D = {xi, yi}i=1^m, where xi ∈ R^n and yi ∈ Y, our goal is to obtain an ensemble classifier that assigns a label to unseen data x in the following way:

y = arg max_{y ∈ Y} Σ_{h ∈ H} p(y|x, h) p(h|D). (19.1)

In this equation, y is the predicted label of x, Y is the set of all possible labels, H is the hypothesis space that contains all possible hypothesis h, and p(·) denotes probability functions. We can see that the Bayes optimal classifier combines all possible base classifiers, i.e., the hypotheses, by summing up their weighted votes. The posterior probability p(h|D) is adopted to be their corresponding weights.

We assume that training examples are drawn independently. By Bayes’ theorem, the posterior probability p(h|D) is given by:

P(h|D) = p(h)p(D|h)/p(D) = p(h)Π_{i=1}^m p(xi|h)/p(D). (19.2)

In this equation, p(h) is the prior probability reflecting the degree of our belief that h is the “correct” model prior to seeing any data. p(D|h) = Π_{i=1}^m p(xi|h) is the likelihood, i.e., how likely the given training set is generated under the model h. The data prior p(D) is the same for all hypotheses, so it could be ignored when making the label predictions.

To sum up, Bayes optimal classifier makes a prediction for x as follows:

y = arg max_{y ∈ Y} Σ_{h ∈ H} p(y|x, h) p(D|h) p(h). (19.3)

By this approach, all the models are combined by considering both prior knowledge and data likelihood. In other words, the Bayes optimal classifier combines all the hypotheses in the hypothesis space, and each hypothesis is given a weight reflecting the probability that the training data would be sampled under the hypothesis if that hypothesis were true. In [61], it is pointed out that Bayes optimal classifier can reach optimal classification results under Bayes theorem, and on average, no other ensemble method can outperform it.

Although Bayes optimal classifier is the ideal ensemble method, unfortunately, it cannot be practically implemented. The prior knowledge about each model p(h) is usually unknown. For most tasks, the hypothesis space is too large to iterate over and many hypotheses only output a predicted label rather than a probability. Even though in some classification algorithms, it is possible to estimate the probability from training data, computing an unbiased estimate of the probability of the training data given a hypothesis, i.e., p(D|h), is difficult. The reason is that when we calculate