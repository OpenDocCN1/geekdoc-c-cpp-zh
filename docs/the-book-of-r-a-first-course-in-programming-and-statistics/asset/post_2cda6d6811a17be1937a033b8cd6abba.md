
In Exercise 21.2, you accessed the trees data frame in the faraway package. After loading the package, access the ?trees help file; you'll find the volume and girth measurements you used earlier, as well as data on the height of each tree.

- d. Without using any transformations of the data, fit and inspect a main-effects-only model for predicting volume from girth and height. Then, fit and inspect a second version of this model including an interaction.

- e. Repeat(d), but this time use the log transformation of all variables. What do you notice about the significance of the interaction between the untransformed and transformed models? What does this suggest about the relationships in the data?

Turn back to the mtcars data set and remind yourself of the variables in the help file mtcars.

- f. Fit a linear model for mpg based on a two-way interaction between hp and factor(cyl) and their main effects, as well as a main effect for wt. Produce a summary of the fit.

- g. Interpret the estimated coefficients for the interaction between horsepower and the (categorical) number of cylinders.

- h. Suppose you're on purchasing a 1970s performance car. Your mother advises you to purchase a "practical and economical car" that's capable of an average MPG value of at least 25. You see three vehicles advertised: car 1 is a four-cylinder, 100 horsepower car that weighs 2100 lbs; car 2 is an eight-cylinder, 210 horsepower that weighs 3900 lbs; and car 3 is a six-cylinder, 200 horsepower car that weighs 2900 lbs.

- i. Use your model to predict the mean MPG for each of the three cars; provide 95 percent confidence intervals. Based on your point estimates only, which would you propose to your mother?

- ii. You still want the most gas-guzzling car you can own with your mother's blessing, so you decide on the choice that the confidence intervals tell you instead. Does this change your choice of vehicle?

# Important Code in this Chapter

| Function/operator | Brief description | First occurrence |
| :--- | :--- | :--- |
| I | Include arithmetic term | Section 21.4.1, p. 505 |
| : | Interaction term | Section 21.5.2, p. 516 |
| * | Cross-factor operator | Section 21.5.3, p. 519 |

# 22
# LINEAR MODEL SELECTION AND DIAGNOSTICS

![](img/b2cfc85cbb129f60fe595a2bae074fe4_560_0.png)

You've now spent a fair amount of time on many aspects of linear regression models. In this chapter, I'll cover how formal R tools and techniques can be used to investigate two other, and no less important, aspects of regression: choosing an appropriate model for your analysis and assessing the validity of the assumptions you've made.

## 22.1 Goodness-of-fit vs. Complexity

The overarching goal of fitting any statistical model is to faithfully represent the data and the relationships held within them. In general, fitting statistical models boils down to a balancing act between two things: goodness-of-fit refers to the goal of obtaining a model that represents the relationships between the response and the predictor (or predictors). Complexity describes how complicated a model is; this is always tied to the number of terms in the model that require estimation—the inclusion of more predictors and additional functions (such as polynomial transformations and interactions) leads to a more complex model.

### 22.1.1 Principle of Parsimony

Statisticians refer to the balancing act between goodness-of-fit and complexity as the principle of parsimony, where the goal of the associated model selection is to find a model that's as simple as possible (in other words, with relatively low complexity), without sacrificing much goodness-of-fit. We'd say a model that satisfies this notion is a parsimonious fit. You'll often hear about choosing the "best" model—they're actually referring to the idea of parsimony.

So, how do you decide to draw the line on such a balance? Naturally, statistical significance plays a role here—and model selection simply comes to assessing the significance of the effect of predictors or functions of predictors on the response. In an effort to impart some amount of objectivity to such a process, you can use systematic selection algorithms, such as the you'll learn about in Section 22.2, to decide between multiple explanatory variables and any associated functions.

### 22.1.2 General Guidelines

Performing any kind of model selection or comparing several models against another involves decision making the inclusion of available predictor variables. On this topic, there are several guidelines you should always follow.

- First, it's important to remember that you can't remove individual levels of a categorical predictor in a given model; this makes no sense. In other words, if one of the nonreference levels is statistically significant but all others are nonsignificant, you should treat the categorical variable, as a whole, as making a statistically contribution to the determination of the mean response. You should only consider entire removal of that categorical predictor if all nonreference coefficients are associated with a lack of evidence (against being zero). This also holds for interactive terms involving categorical predictors.

- If an interaction is present in the fitted model, all-order interactions and main effects of the relevant predictors must remain in the model. This was touched upon in Section 21.5.1, when I discussed interpretation of interactive effects as augmentations of lower-order effects. As an example, you should only consider removing the main effect of a predictor if there are no interaction terms present in the fitted model involving that predictor (even if it has a high p-value).

- In models you've used a polynomial transformation of a certain explanatory variable (refer to Section 21.4.1), keep all lower-order polynomial terms in the model if the highest is deemed significant. A model containing an order 3 polynomial transformation in a predictor, for example, must also include the order 1 and order 2 transformations of that variable. This is because of the mathematical behavior of polynomial functions—only by explicitly separating the linear, quadratic, and cubic (and so on) effects as distinct terms you can avoid confounding effects with one another.

## 22.2 Model Selection Algorithms

The job of a model selection algorithm is to sift through your available explanatory variables in systematic fashion in order to establish which are best to jointly describe the response, as opposed to fitting models by examining specific combinations of predictors in isolation, as you've done so far.

Model selection algorithms can be controversial. There are several different methods, and no single approach is universally appropriate for every regression model. Different selection algorithms can result in different final models, as you'll see. In many cases, researchers will have additional information or knowledge about the problem that influences the decision—for example, certain predictors must always be included. This must be considered at the same time as other complications, such as the possibility of interactions or unobserved lurking variables and the need to ensure any fitted model is valid (which you'll look at in Section 22.3).

It's helpful to keep in mind this famous quote from statistician George Box (1919–2013): "All models are wrong, but some are useful." Any fitted model you produce can never be assumed to be the truth, but a model that's fitted carefully and thoroughly can reveal interesting features of the data and have the potential to provide quantitative estimates thereafter.

### 22.2.1 Nested Comparisons: The Partial F-Test

The F test is probably the most direct way to compare several models. It looks at two or more nested models, where the smaller, less complex model is a reduced version of the larger, more complex model. Let's say you have two linear regression models as:

$\hat{y}_{red} = \hat{�eta}_0 + \hat{�eta}_1x_1 + \hat{�eta}_2x_2 + \dots + \hat{�eta}_p x_p$

$\hat{y}_{full} = \hat{�eta}_0 + \hat{�eta}_1x_1 + \hat{�eta}_2x_2 + \dots + \hat{�eta}_p x_p + \dots + \hat{�eta}_q x_q$

Here, the reduced model, predicting $\hat{y}_{red}$, has $p$ predictors, plus one intercept. The full model, predicting $\hat{y}_{full}$, has $q$ predictor terms. The notation implies that $q > p$ and, along with the standard inclusion of an intercept $\hat{�eta}_0$, the full model involves all $p$ predictors of the reduced model defined by $\hat{y}_{red}$, as well as $q - p$ additional terms. This emphasizes the fact that the model for $\hat{y}_{red}$ is nested within $\hat{y}_{full}$.

It's important to note that increasing the number of predictors in a regression model will always improve $R^2$ and any other measures of
