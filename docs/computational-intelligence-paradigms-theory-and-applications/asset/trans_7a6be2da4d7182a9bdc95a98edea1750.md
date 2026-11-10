
```matlab
disp(gpols_result{1,1});
disp(gpols_result{popu,1});
% GP loops
for c = 2:20,
    % iterate
    popu = gpols_mainloop(popu,X,Y,[],opt);
    % info
    disp(gpols_result{popu,1});
end

% Result
[s,tree] = gpols_result(popu,2);
disp(s);
```

| 迭代 | 适应度 | 解 |
| --- | --- | --- |
| 1. | 0.284622 | (y(k-2))+((u(k-2))+(u(k-1))) |
| 2. | 0.284622 | (y(k-2))+((u(k-2))+(u(k-1))) |
| 3. | 0.284622 | (y(k-2))+((u(k-2))+(u(k-1))) |
| 4. | 0.683562 | (y(k-2))+((u(k-1))*(u(k-1))) |
| 5. | 0.683562 | (y(k-2))+((u(k-1))*(u(k-1))) |
| 6. | 0.894455 | (y(k-1))+((u(k-1))*(u(k-1))) |
| 7. | 0.894455 | (y(k-1))+((u(k-1))*(u(k-1))) |
| 8. | 0.894455 | (y(k-1))+((u(k-1))*(u(k-1))) |
| 9. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 10. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 11. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 12. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 13. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 14. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 15. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 16. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 17. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 18. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 19. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |
| 20. | 0.903012 | ((y(k-2))+((u(k-1))*(u(k-1))))+((u(k-1))*(u(k-2))) |

```text
fitness: 0.903012, mse: 0.001285
-0.777391 * ((u(k-1))*(u(k-2))) +
-0.370513 * (y(k-2)) +
1.059709 * ((u(k-1))*(u(k-1))) +
-0.047268
```

GP-OLS 算法生成参数线性模型或多项式模型，仿真结果表明，所提出的工具为非线性过程选择输入-输出模型结构提供了一种高效、快速的方法。

### 14.9.3 示例 3 – 符号回归问题

使用遗传编程工具箱

以下程序运行一个符号回归问题（二次多项式），使用 100 个个体、25 代，自动调整算子概率，在运行过程中绘制若干图形，并在运行结束后再绘制两个附加图形。

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
% OPNAME - the name of the operator to use (string)
% NPARENTS - the number of parents required by the
% operator
% NCHILDREN - the number of children produced by
% the operator
% Output arguments:
% PARAMS - the updated algorithm running parameters
% (struct) %

params.operatornames={};
params.operatorparents={};
params.operatorchildren={};

params.initialfixedprobs=[];
params.initialvarprobs=[];

params = addoperators(params,varargin);

% - - - - - - - - End of setoperators - - - - - - - -

function [vars,best]=gplab(g,varargin)
% Input arguments:
%   NGENS - the number of generations to run
%           the algorithm (integer)
%   POPSIZE - the number of individuals in the
%             population (integer)
%   PARAMS - the algorithm running parameters (struct)
%   VARS - the algorithm variables (struct)
%     VARS.POP - the current population
%     VARS.PARAMS - the algorithm running parameters =
%                   PARAMS
%     VARS.STATE - the current state of the algorithm
% Output arguments:
%   VARS - the algorithm variables (struct) - see Input
%          arguments
%   BEST - the best individual found in the run
%          (struct)

if (nargin<2) || (nargin>3)

error('GPLAB: Wrong number of input arguments. Use either gplab(ngens, vars) to continue a run, or gplab(ngens, popsize, [optional params]) to start a run')

...

elseif isstruct(varargin{1})
    % argument 1: the number of additional generations to run
    % argument 2: the algorithm variables
    if ~(isvalid(g,'posit'))
        error('GPLAB: The first argument must be an integer greater than 0.')
    end
    start=0;
    continuing=1;
    vars=varargin{1};
    n=vars.state.popsize;
    level=vars.state.maxlevel;
    ginic=vars.state.generation+1; % start generation number
    gend=ginic-1+g; % end generation number
else
    % argument 1: the number of generations to run
    % argument 2: the number of individuals in the population
    % argument 3: (optional) the parameters of the algorithm

    if ~(isvalid(g,'special_posint') && isvalid(varargin{1}, 'posit') && varargin{1}>=2)

        error('GPLAB:The first two arguments must be integers, and the second >1')

    end
    start=1;
    continuing=0;
    n=varargin{1};
    if nargin==3
        vars.params=varargin{2};
    else
        vars.params=[];
    end
    vars.state=[];
    vars.data=[];
    ginic=1; % start generation number
    gend=g; % end generation number
end

% check parameter variables:
vars.params=checkvarsparams(start,continuing,
vars.params,n);

% check data variables:
[vars.data,vars.params]=checkvarsdata(start,
continuing,vars.data,vars.params);

% check state variables:
[vars.state,vars.params]=checkvarsstate(start,
continuing,vars.data,vars.params,vars.state,n,g);

% initialize random number generator (see help on
RAND):
rand('state',sum(100*clock));
fprintf('\n Running algorithm...\n');

% initiate graphics:
% (if we're not going to run generations or draw
history,
% don't initiate the graphics)
if ~isempty(vars.params.graphics) && (ginic <= gend || continuing)
    gfxState=graphicsinit(vars.params);
end

% initial generation:

if start
    [vars.pop,vars.state]=genpop(vars.params,vars.state,vars.data,n);
    if strcmp(vars.params.savetofile,'firstlast') || ...
    strcmp(vars.params.savetofile,'every10') || ...
    strcmp(vars.params.savetofile,'every100') || ...
    strcmp(vars.params.savetofile,'always')
        saveall(vars);
    end
    if ~strcmp(vars.params.output,'silent')
        fprintf(' # Individuals: %d\n', vars.state.popsize);
        if strcmp(vars.params.survival,'resources')
            fprintf('MaxResources: %d\n', vars.state.maxresources);
        end
        fprintf('UsedResources: %d\n', vars.state.usedresources);
        fprintf('Best so far: %d\n', vars.state.bestsofar.id);
        fprintf('Fitness: %f\n', vars.state.bestsofar.fitness);
        if vars.params.usetestdata
            fprintf(' Test fitness: %f\n', vars.state.bestsofar.testfitness);
        end
        fprintf(' Depth: %d\n', vars.state.bestsofar.level);
        fprintf(' Nodes: %d\n\n', vars.state.bestsofar.nodes);
    end
    % (if we're not going to run generations, don't start
    % the graphics:)
    if ~isempty(vars.params.graphics) && ginic<=gend
        gfxState=graphicsstart(vars.params,vars.state,
                     gfxState);
    end
end

if continuing
    if ~isempty(vars.params.graphics)
       gfxState=graphicscontinue(vars.params,vars.state,
                     gfxState);
    end
end

sc=0;

% generations:

for i=ginic:gend

    % stop condition?
    sc=stopcondition(vars.params,vars.state,vars.data);
    if sc
       % unless the option is to never save, save
       % the algorithm variables now:
       if ~strcmp(vars.params.savetofile,'never')
           saveall(vars);
       end
       break % if a stop condition has been reached,
             % skip the for cycle
    end

    % new generation:

    [vars.pop,vars.state]=generation(vars.pop,vars.params,
vars.state, vars.data);
```
