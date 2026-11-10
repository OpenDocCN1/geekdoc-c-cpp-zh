
```matlab
% save to file?
if (strcmp(vars.params.savetofile,'firstlast') && img) ||
   (strcmp(vars.params.savetofile,'every10') && rem(i,10)==0) ||
   (strcmp(vars.params.savetofile,'every100') && rem(i,100)==0) ||
   strcmp(vars.params.savetofile,'always')
    saveall(vars);
end

% textual output:
if ~strcmp(vars.params.output,'silent')
    fprintf(' # Individuals: %d\n',vars.state.popsize);
    if strcmp(vars.params.survival,'resources')
        fprintf(' MaxResources: %d\n',vars.state.maxresources);
    end
    fprintf(' UsedResources: %d\n',vars.state.usedresources);
    fprintf(' Best so far: %d\n',vars.state.bestsofar.id);
    fprintf(' Fitness: %f\n',vars.state.bestsofar.fitness);
    if vars.params.usetestdata
        fprintf(' Test fitness: %f\n',vars.state.bestsofar.testfitness);
    end
    fprintf(' Depth: %d\n',vars.state.bestsofar.level);
    fprintf(' Nodes: %d \n\n',vars.state.bestsofar.nodes);
end

% plots:
if ~isempty(vars.params.graphics)
    gfxState=graphicsgenerations(vars.params, vars.state, gfxState);
end

end % for i=gnic:gend

% messages regarding the stop condition reached:
if sc
    if vars.state.generation==0
        fprintf('\n Stop condition #%d was reached after initial generation.\n', sc);
    else
        fprintf('\n Stop condition #%d reached after generation %d.\n', sc, vars.state.generation);
    end
else
    fprintf('\n Maximum generation %d was reached.\n', vars.state.generation);
end

best=vars.state.bestsofar;
vars.state.keepvals=[];
% clear memory, we don't want to save all this!

fprintf('\nDone!\n\n');

% - - - - - - - - - End of gplab - - - - - - - - - -

function accuracy_complexity(vars,offsets,bw,sizexy)
% Input arguments:
% VARS - all the variables of the algorithm (struct)
% OFFSETS - the offsets for each line, [] for no offset
% BLACKWHITE - the flag to draw a bw or color plot (boolean)
% SIZEPLOT - the x and y size of plot, [] for default (1x2 matrix)
h=vars.state.bestsofarhistory;

if isempty(offsets)
    fitoffset=0;
    leveloffset=0;
    nodesoffset=0;
else
    fitoffset=offsets(1);
    leveloffset=offsets(2);
    nodesoffset=offsets(3);
end

if isempty(sizexy)
    sizexy(1)=0;
    sizexy(2)=0;
end

for i=1:size(h,1)
    g(i)=h(i,1);
    f(i)=h(i,2).fitness;
    l(i)=h(i,2).level;
    n(i)=h(i,2).nodes;
    % noruegueses fizeram
    % n(i)=nodes(h(i,2).tree);
end
g=g';
f=f'+fitoffset;
l=l'+leveloffset;
n=n'+nodesoffset;

ff=figure;
set(ff,'Color',[1 1 1]);
if sizexy(1)<=0
    sizexy(1)=400;
end
if sizexy(2)<=0
    sizexy(2)=350;
end

set(ff,'Position',[200 250 sizexy(1) sizexy(2)])
hold on
title('Accuracy versus Complexity');
xlabel('generation');

if fitoffset~=0
    if fitoffset<0
        ylab1=strcat('fitness',int2str(fitoffset));
    else
        ylab1=strcat('fitness+',int2str(fitoffset));
    end
else
    ylab1='fitness';
end

if leveloffset~=0
    if leveloffset<0
        ylab2=strcat('level',int2str(leveloffset));
    else
        ylab2=strcat('level+',int2str(leveloffset));
    end
else
    ylab2='level';
end

if nodesoffset~=0
    if nodesoffset<0
        ylab3=strcat('nodes',int2str(nodesoffset));
    else
        ylab3=strcat('nodes+',int2str(nodesoffset));
    end
else
    ylab3='nodes';
end

ylaball=[ylab1 ' ' ylab2 ' ' ylab3];
ylabel(ylaball);

if bw
    plot(g,f,'k.-',g,l,'k--',g,n,'k+-');
else
    plot(g,[f,l,n],'-');
end
legend(ylab1,ylab2,ylab3);

% - - - - - End of accuracy_complexity - - - - -

function plotpareto(vars) %
% Input arguments:
%   VARS - all the variables of the algorithm (struct)
% Output arguments:
%   none
%

for im=1:length(vars.pop)
    if isempty(vars.pop(im).nodes)
        vars.pop(im).nodes=nodes(vars.pop(im).tree);
    end
end

% build pareto front variable:
paretofront=[];
paretofront(1).fitness=[];
for solution=vars.pop
    while length(paretofront)<solution.nodes
        paretofront(end+1).ind=[];
    end
    if isempty(paretofront(solution.nodes).fitness)|| ...
       ((vars.params.lowerisbetter&&...
       solution.fitness<paretofront(solution.nodes).fitness)|| ...
       (~vars.params.lowerisbetter&&...
       solution.fitness>paretofront(solution.nodes).fitness))
        % cross validation
        if vars.params.usetestdata
            testindividual=calcfitness(solution, vars.params.vars, data.test, vars.state, 1);
            % (1 = test data)
            solution.testfitness=testindividual.fitness;
        end
        paretofront(solution.nodes).fitness=solution.fitness;
        paretofront(solution.nodes).ind=solution;
        if vars.params.usetestdata
            paretofront(solution.nodes).testfitness=solution.testfitness;
        end
    end
end
% collect fitness and #nodes:
y=[paretofront.fitness];
x=[];
for i=1:size(paretofront,2)
    if ~isempty(paretofront(i).ind)
        x=[x i];
    end
end
if length(y) ~=length(x)
    error('','internal error');
end
% Compute pareto front:
best=[];
bestind=[];
sofar=[];
for i=1:length(y)
    if i==1 | y(i) >sofar
        sofar=y(i);
        best=[best sofar];
        bestind=[bestind x(i)];
    end
end

hold on
title('Pareto front');
xlabel('nodes');
ylabel('fitness');
% plot:
plot(x,y,'o-',bestind,best,'ro-');
plot([vars.pop.nodes],[vars.pop.fitness],'g*');
if vars.params.usetestdata
    plot(x,[paretofront.testfitness],'m-');
    legend('best for #nodes','pareto front','current population','test fitness');
else
    legend('best for #nodes','pareto front','current population');
end
hold off
% - - - - - - - - - End of plotpareto - - - - - - - - -

function drawtree(tree,titletxt)
%
% Input arguments:
% TREE - a GPLAB tree (struct)
% TITLE - title of the tree figure (optional,string)
% Output arguments:
% none
%
% Set tree titles
if nargin <2
    titletxt = 'Displaying GPLAB-tree found';
end
% Using new figure to display tree
h=figure; % new figure for this particular tree
set(h,'name',titletxt);

% First, count nodes
[tree, count] = walkTreeDepthFirst(tree, 'countLeaves', [], 0, 0);
state.nodeCount = count;
state.yDist = -1;
% Position leaves (equally spaced)
[tree, state]=walkTreeDepthFirst(tree, 'positionLeaves', [], 0, state);
% Position parents (midway between kids)
[tree, state] = walkTreeDepthFirst(tree, [], 'positionParents', 0, 0, state);
% Draw tree
[tree,state]=walkTreeDepthFirst(tree, [], 'drawNode', 0, 0);

axis('off')

function [tree, state] = walkTreeDepthFirst(tree, preDive, postDive, initialDepth, state)
% Calls preDive(tree, depth, state), enters subnodes,
% calls postDive(tree,depth,state). Useful for walking
% the tree.
if ~isempty(preDive)
    [tree, state] = feval(preDive, tree, initialDepth, state);
end

for i = 1:length(tree.kids)
    [tree.kids{i}, state] = walkTreeDepthFirst(tree.kids{i}, preDive, postDive, initialDepth + 1, state);
end
if ~isempty(postDive)
    [tree, state] = feval(postDive, tree, initialDepth, state);
end

function [tree,count]=countLeaves(tree,depth,count)
if isempty(tree.kids)
    tree.index = count;
    count = count + 1;
end

function [tree,state]=positionLeaves(tree,depth,state)
if isempty(tree.kids)
    if state.nodeCount <= 1
        tree.X = 0;
    else
        tree.X = tree.index / (state.nodeCount - 1);
    end
    tree.Y = depth * state.yDist;
end

function [tree,state]=positionParents(tree,depth,state)
if ~isempty(tree.kids)
    x = [];
    for i = 1:length(tree.kids)
        kid = tree.kids{i};
        x = [x kid.X];
    end
    tree.X = mean(x);
    tree.Y = depth * state.yDist;
end

function [tree, state] = drawNode(tree, depth, state)
if ~isempty(tree.kids)
    for i = 1:length(tree.kids)
        kid = tree.kids{i};
        line([tree.X kid.X], [tree.Y kid.Y]);
    end
    line(tree.X, tree.Y, 'marker', '*', 'markersize', 8)
    opText = tree.op;
    text(tree.X, tree.Y, [' ' opText], 'HorizontalAlignment', 'left', 'interpreter', 'none')
else
```
