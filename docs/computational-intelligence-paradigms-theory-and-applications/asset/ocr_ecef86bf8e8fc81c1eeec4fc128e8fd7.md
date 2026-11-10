# # Chapter 10

# ## Neuro-Fuzzy Modeling Using MATLAB

In this chapter, MATLAB illustrations are given on ANFIS, Classification and Regression trees, Fuzzy c-means clustering algorithms, Fuzzy ART Map, and Simulink models on Takagi-Sugeno inference systems.

# ### 10.1 Illustration 1 - Fuzzy Art Map

```
~~~matlab
Simplified Fuzzy Art Map

% SFAM usage demo.
%
function sfam.demo

% load data
load demodata

% create network
net = create_network(size(data,2))

% change some parameters as you wish
% net.epochs = 1;

% train the network
tnet = train(data, labels, net, 100)

% test the network on the testdata
r = classify(testdata, tnet, testlabels, 10);

% compute classification performance
printf(1,'Hit rate: % f \ n', sum(r' ==
~~~
```