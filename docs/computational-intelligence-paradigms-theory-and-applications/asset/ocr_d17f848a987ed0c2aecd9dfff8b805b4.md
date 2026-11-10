# ### 14.9.3 Illustration 3 – Symbolic Regression Problem
Using Genetic Programming Toolbox

The following program runs a symbolic regression problem (the quadratic polynomial) with 100 individuals for 25 generations, with automatic adaptation of operator probabilities, drawing several plots in runtime, and finishing with two additional post-run plots.

```
```matlab
-----------------------------------------------------------
% Main Program
-----------------------------------------------------------
fprintf('Running symbolic regression demo...');
p=presetparams;

p=setoperators(p,'crossover',2,2,'mutation',1,1);
p.operatorprobstype='variable';
p.minprob=0;

p.datafilex='quartic.x.txt';
p.datafiley='quartic.y.txt';

p.usetestdata=1;
p.testdatafilex='exp.x.txt';
p.testdatafiley='exp.y.txt';

p.calcdiversity='uniquegen';
p.calccomplexity=1;
p.graphics={'plotfitness','plotdiversity','plotcomplexity',
'plotoperators'};
p.depthsnodes='2';

[v,b]=gplab(25,50,p);

desired_obtained(v,[],1,0,[]);
accuracy_complexity(v,[],0,[]);

figure
plotpareto(v);

drawtree(b.tree);

-----------------------------------------------------------
% Subprograms
-----------------------------------------------------------
function params=setoperators(params,varargin)
%
% Input arguments:
%   PARAMS - the algorithm running parameters (struct)
```
```