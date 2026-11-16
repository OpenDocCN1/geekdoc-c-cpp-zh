
![](img/d3c00252180686426c9e63ab889b535b_139_0.png)

![](img/d3c00252180686426c9e63ab889b535b_139_1.png)

### Figure 5.4: Gaussian kernel.

![](img/d3c00252180686426c9e63ab889b535b_139_2.png)

![](img/d3c00252180686426c9e63ab889b535b_139_3.png)

### Figure 5.5: Exponential kernel.

The exponential kernel is also an intuitive similarity measure. Equality of x and y is, however, more emphasized than by the Gaussian kernel with the exponential kernel being sharply peaked at zero. Figure 5.5 gives two examples for different choices of $\theta_2$.

Some of the other kernels are shown in Figure 5.6. The multiquadric and thin plate spline kernels are contra-intuitive similarity measures, since their value increases as the distance between x and y increases. Also their Gram matrices are not necessarily positive semi-definite. With the addition of a polynomial kernel, they can be made to be positive definite (see for example [6]).

The parameter $\alpha$ in the rational quadratic kernel

```
$k(\mathbf{x}, \mathbf{y}) = \theta_1^2 \left( 1 + \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\alpha\theta_2^2} \right)^{-\alpha}$
```

is known as *scale-mixture parameter*. As $\alpha$ increases, the error in the approximation

```
1 + \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\alpha \theta_2^2} = \exp \left( \frac{\|\mathbf{x} - \mathbf{y}\|^2}{2\alpha \theta_2^2} \right) + O(\alpha^2)
```

decreases for fixed $\mathbf{x}$ and $\mathbf{y}$. Therefore, as $\alpha$ approaches infinity, the rational quadratic kernel becomes the Gaussian kernel. Using expansions, the rational quadratic kernel can be viewed as an infinite sum of Gaussian kernel with different characteristic length scales. Radial basis functions have many theoretical properties which can influence their performance; see for example [6].

All feature dimensions are treated equally in the kernel definitions so far. However, one feature might be more spread out than another. One possibility to tackle this is, instead of using the characteristic length scale $\theta_2$, to have a separate length scale $\theta_{m+1}$ for each feature dimension m = 1, ..., M. That is, instead of $\|\mathbf{x} - \mathbf{y}\|^2 / \theta_2^2$, we have

```
\left( \frac{x_1 - y_1}{\theta_2} \right)^2 + \dots + \left( \frac{x_M - y_M}{\theta_{M+1}} \right)^2 .
```

![](img/d3c00252180686426c9e63ab889b535b_140_0.png)

- (a) Multiquadric kernel, y = (0, 0), \theta_1 = \theta_2 = 1.

![](img/d3c00252180686426c9e63ab889b535b_140_1.png)

- (b) Inverse multiquadric kernel, y = (0, 0), \theta_1 = \theta_2 = 1.

![](img/d3c00252180686426c9e63ab889b535b_140_2.png)

- (c) Rational quadratic kernel, y = (0, 0), \theta_1 = 10, \theta_2 = 1, \alpha = 2.

![](img/d3c00252180686426c9e63ab889b535b_140_3.png)

- (d) Thin plate spline kernel, y = (0, 0), \theta_1 = 0.1, \theta_2 = 1.

### Figure 5.6: Radial basis function kernels.

![](img/d3c00252180686426c9e63ab889b535b_141_0.png)

### Figure 5.7: Support Vector Machine classification with Gaussian kernel.

Increasing the number of parameters to be chosen is, however, better avoided. Instead, the training data is *standardized*. For each feature dimension, the training data, $\mathbf{v}_1, \dots, \mathbf{v}_N$, is shifted by the mean and scaled by the standard deviation. Writing $\mathbf{v}_m = (v_{1m}, \dots, v_{Nm})^T$, for $m = 1, \dots, M$ we calculate

```
$$\mu_m = \frac{1}{N} \sum_{n=1}^N v_{nm} \text{ and } \sigma_m^2 = \frac{1}{N} \sum_{n=1}^N (v_{nm} - \mu_m)^2.$$
```

The standardized training data is then $\tilde{\mathbf{v}}_1, \dots, \tilde{\mathbf{v}}_N$ with

```
$$\tilde{v}_{nm} = \frac{v_{nm} - \mu_m}{\sigma_m}.$$
```

The research on kernels is an active field with new kernels being developed for specific applications. Their usefulness lies in the fact that they do not need to be defined over $\mathbb{R}^M \times \mathbb{R}^M$, but can be defined over different categories of objects. An example are string kernels [37] and graph kernels [32]. It all comes down to defining a suitable similarity measure between objects.

The MATLAB code in Listing 5.2 applies a kernel Support Vector Machine to Fisher's iris data using the Gaussian kernel. The results can be seen in Figure 5.7.

```
load fisheriris
% extract two attributes
pl = meas(:,3); % petal length
pw = meas(:,4); % petal width
X = [pl,pw];

% determine classes
classes = unique(species);
% classifiers are constructed on the principle of One versus All
% as many classifier as classes are needed
SVMModels = cell(numel(classes),1);
rng(1); % seeding the random number generator for reproducibility

for j = 1:numel(classes)
    % train binary classes for each classifier
    idx = strcmp(species,classes{j});
    % create classifier
    SVMModels{j} = fitcsvm(X,idx,'ClassNames',[false true],...
        'Standardize',true,...
        'KernelFunction','gaussian'); % specifying the kernel
end

% lay grid over the region
d = 0.01;
[x1Grid,x2Grid] = meshgrid(0.8:d:7,0:d:3);
XGrid = [x1Grid(:), x2Grid(:)];
N = size(XGrid,1);
Scores = zeros(N,numel(classes));

% for each grid point calculate the score of each classifier
for j = 1:numel(classes)
    % predict both returns the predicted class labels as well as a
    % score indicating the likelihood of the negative class (false)
    % and positive class (true)
    [~,score] = predict(SVMModels{j}, XGrid);
    Scores(:,j) = score(:,2); % second column contains positive
end % class scores

% classify according to the maximum score
[~,maxScore] = max(Scores,[],2);

% plot classification regions
figure
h(1:3) = gscatter(XGrid(:,1),XGrid(:,2),maxScore,...
    [0.5 0.5 0.5; 0.7 0.7 0.7; 0.9 0.9 0.9]);
hold on
% plot data
h(4:6) = gscatter(pl, pw, species,'rgb','os^');
xlabel('Petal length');
ylabel('Petal width');
legend({'Setosa region','Versicolor region','Virginica region',...
    'Setosa','Versicolor','Virginica'},...
    'Location','Northwest');
axis([0.8 7 0 3])
hold off
```

### Listing 5.2: Support Vector Machine using Gaussian kernels.

![](img/d3c00252180686426c9e63ab889b535b_143_0.png)

### Figure 5.8: k Nearest Neighbour classification.

## 5.3 k Nearest Neighbours

In the previous chapter, we considered classifying samples according to their relationship to samples in the training set. This relation was quantified using kernels. A simple idea is to classify a new sample according to the majority of classes to which its neighbours in the training set belong. Here neighbour is defined as the samples closest with regards to the Euclidean norm, also known as the L2 norm. The number of neighbours considered is denoted by k. The classifier depends on the choice of k. If a small number of neighbours is chosen, then the boundaries between the classes are more irregular, while they are smoother, if k is chosen larger. The technique is known as k Nearest Neighbours (k-NN). Listing 5.3 creates a k Nearest Neighbour classifier and uses it to classify the entire region. Adjusting the parameter specifying the number of neighbours shows the different outcomes. Three new sample points are also generated, their k nearest neighbours marked and ellipses drawn around the nearest neighbours. Figure 5.8 shows the results.

## 5.4 Decision Trees

Another intuitive way to classify are decision trees. These are binary trees consisting of nodes and leaves, also known as terminal nodes. Each non-terminal node has two branches. A sample enters the tree at the root node at the top. At each node, a decision is made based on the value of a single feature. If

```
```matlab
load fisheriris

% Extract two attributes.
pl = meas(:,3); % petal length
pw = meas(:,4); % petal width
X = [pl pw];

% Create classifier.
k = 5
knnModel = fitcknn(X,species,...
    'NumNeighbors',k,...
    'Standardize',true); % standardize data

% Lay grid over the region.
d = 0.01;
[x1Grid,x2Grid] = meshgrid(0:d:7,0:d:3);
XGrid = [x1Grid(:),x2Grid(:)];
N = size(XGrid,1);

% For each grid point calculate the score of each class.
% 'predict' returns the predicted class labels corresponding to the
% minimum misclassification cost, the score (posterior probability)
% and the cost of the expected misclassification cost for
% each class.
[~,score,~] = predict(knnModel,XGrid);

% Classify according to the maximum score.
[~,maxScore] = max(score,[],2);

% Plot classifier regions.
figure
h(1:3) = gscatter(XGrid(:,1),XGrid(:,2),maxScore,...
    [0.5 0.5 0.5; 0.7 0.7 0.7; 0.9 0.9 0.9]);
hold on

% Plot data.
h(4:6) = gscatter(pl, pw, species,'rgb','o*^');
xlabel('Petal length');
ylabel('Petal width');
legend(h,{'Setosa region','Versicolor region','Virginica region',...
    'Setosa','Versicolor','Virginica'},...
    'Location','Northwest');
axis([0.8 7.0 0 3])

% Plot new points with ellipses containing nearest neighbours.
newpoints = [2.5 .75;...
    5 2;...
    2 1.4];
plot(newpoints(:,1),newpoints(:,2),'xk','linewidth',1.5);

% Find nearest neighbours.
[idx,d] = knnsearch(X,newpoints,...
    'K',k,...
    'Distance','seuclidean'); % Euclidean distance on standardized data

% Mark neighbours.
plot(newpoints(idx,1), newpoints(idx,2),'markersize',10);

% Plot ellipses.
for i=1:3
    a = knnModel.Sigma < -d(i,end) % scale standardized coordinates
    newpoints(i,:) = a % corner of rectangle containing ellipse
    % Draw an ellipse around the nearest neighbours.
    h = rectangle('position',[c,x2s(1),x2s(2),...
        'curvature',[1 1],'LineStyle','--');
end
hold off
```
```

### Listing 5.3: k Nearest Neighbours.
