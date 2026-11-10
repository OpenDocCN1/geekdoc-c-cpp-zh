```
```
% Generate a random symbol (terminate or operate)
% [nodetyp,node] = tree.genrndsymb(p0,nn)
% nodetyp,node <- results
% p0 ->probability of terminate node
% nn ->vector [number of operators, variables]
%
if rand<p0,
    nodetyp = 2;
else
    nodetyp = 1;
end
node = floor(nn(nodetyp)*rand)+1;
```
```

# ## 14.5 Genetic Programming in Machine Learning

In several fields like artificial intelligence, machine learning, or symbolic processing, several problems originate whose resolution can be considered as the search of a computer program, within a space of feasible programs that produce a few desired outputs from the inputs. This search should be executed in such a way that the searched program is the more capable for the problem that is considered. The genetic programming (GP) paradigm furnishes the appropriate framework to implement this type of search in an efficient and flexible mode, because it can adapt to any problem type.

The paradigm of genetic programming is based on the principle of survival of fittest (C. Darwin). Beginning from a randomly-generated initial population, it acquires populations adopting this principle. The new individuals are a product of genetic operations on the current population's better individuals. In association with the genetic algorithms (GAs), GP contributes the philosophy and the characteristics of being heuristic and stochastic.

Within the area of the machine learning, various paradigms are concentrated toward the resolution of problems. In each paradigm the applied structures are different.

# ### Connectionist Model

Here the value of the signal is amplified or diminished with strengths known as weights which are real valued. The solution to the problem is