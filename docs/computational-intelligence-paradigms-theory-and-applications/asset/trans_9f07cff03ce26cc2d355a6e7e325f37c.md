
- 21. 简要解释进化策略（ES）中的变异和重组。
- 22. 进化策略搜索中的收敛准则是什么？
- 23. 区分进化规划（EP）和进化策略（ES）。
- 24. 简述进化计算（EC）的几个优点和缺点。

## 第12章

### 使用MATLAB实现的进化算法

本章给出了已求解的MATLAB程序，以说明进化计算在优化、比例-微分控制器、多目标优化和函数最小化等问题中的实现。

### 12.1 示例1：差分进化优化器

```matlab
%**************************************************
% Script file for the initialization and run of the differential
% evolution optimizer
%**************************************************

% F_VTR    "Value To Reach" (stop when ofunc < F_VTR)
F_VTR = -10;

% I_D      number of parameters of the objective
%          function
I_D = 2;

% FVr_minbound,FVr_maxbound   vector of lower
% and bounds of initial population
%          the algorithm seems to work especially
% well if [FVr_minbound,FVr_maxbound]
% covers the region where the global minimum is
%          expected
%*** note: these are no bound constraints!! ***
FVr_minbound = -3*ones(1,I_D);
FVr_maxbound = 3*ones(1,I_D);
I_bnd_constr = 0; % 1: use bounds as bound
% constraints, 0: no bound constraints

% I_NP number of population members
I_NP = 15; % pretty high number -
% needed for demo purposes only

% I_itermax maximum number of iterations(generations)
I_itermax = 50;

% F_weight DE-stepsize F_weight ex [0, 2]
F_weight = 0.85;

% F_CR crossover probability constant ex [0, 1]
F_CR = 1;

% I_strategy 1 -->DE/rand/1:
%           the classical version of DE.
%           2 -->DE/local-to-best/1:
%           a version which has been used by quite a number
%           of scientists. Attempts a balance between robustness
%           and fast convergence.
%           3 -->DE/best/1 with jitter:
%           tailored for small population sizes and fast convergence.
%           Dimensionality should not be too high.
%           4 -->DE/rand/1 with per-vector-dither:
%           Classical DE with dither to become even more robust.
%           5 -->DE/rand/1 with per-generation-dither:
%           Classical DE with dither to become even more robust.
%           Choosing F_weight = 0.3 is a good start here.
%           6 -->DE/rand/1 either-or-algorithm:
%           Alternates between differential mutation and three-point-
%           recombination.

I_strategy = 3;

% I_refresh intermediate output will be produced after
%       "I_refresh" iterations. No intermediate
%       output will be produced if I_refresh is <1
I_refresh = 1;

% I_plotting    Will use plotting if set to 1. Will
% skip plotting otherwise.
I_plotting = 1;

%--Problem dependent constant values for plotting--
if (I_plotting == 1)
    FVc.xx = [-3:0.25:3]';
    FVc.yy = [-3:0.25:3]';

    [FVrX,FM_y] = meshgrid(FVc.xx',FVc.yy');
    FM.meshd = peaks(FVrX,FM_y);

    S.struct.FVc.xx = FVc.xx;
    S.struct.FVc.yy = FVc.yy;
    S.struct.FM.meshd = FM.meshd;
end

S.struct.I_NP           = I_NP;
S.struct.F_weight       = F_weight;
S.struct.F_CR           = F_CR;
S.struct.I_D            = I_D;
S.struct.FVr_minbound   = FVr_minbound;
S.struct.FVr_maxbound   = FVr_maxbound;
S.struct.I_bnd_constr   = I_bnd_constr;
S.struct.I_itermax      = I_itermax;
S.struct.F_VTR          = F_VTR;
S.struct.I_strategy     = I_strategy;
S.struct.I_refresh      = I_refresh;
S.struct.I_plotting     = I_plotting;

%******************************************************
% Start of optimization
%******************************************************

[FVr_x,S_y,I_nf] = deopt('objfun',S.struct)
```

### 使用的子函数

```matlab
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Minimization of a user-supplied function with respect
% to x(1:I_D),
% using the differential evolution (DE) algorithm.
% DE works best if [FVr_minbound,FVr_maxbound] covers
% the region where the
% global minimum is expected. DE is also somewhat
% sensitive to
% the choice of the stepsize F_weight. A good initial
% guess is to
% choose F_weight from interval {0.5, 1], e.g. 0.8.
% F_CR, the crossover
% probability constant from interval [0, 1] helps to
% maintain
% the diversity of the population but should be close to
% 1 for most.
% practical cases. Only separable problems do better with
% CR close to 0
% If the parameters are correlated, high values of F_CR
% work better.
% The reverse is true for no correlation.
% The number of population members I_NP is also not very
% critical. A
% good initial guess is 10*I_D. Depending on the
% difficulty of the
% problem I_NP can be lower than 10*I_D or must be higher
% than
% 10*I_D to achieve convergence.
%
% deopt is a vectorized variant of DE which, however,
% has a
% property which differs from the original version of DE:
% The random selection of vectors is performed by
% shuffling the
% population array. Hence a certain vector can't be
% chosen twice
% in the same term of the perturbation expression.
% Due to the vectorized expressions deopt executes
% fairly fast
% in MATLAB's interpreter environment.
%
% Parameters: fname (I) String naming a function f(x,y)
% to minimize.
% S.struct (I) Problem data vector (must remain
% fixed during the
% minimization ).

I_NP        = S.struct.I_NP;
F_weight    = S.struct.F_weight;
F_CR        = S.struct.F_CR;
I_D         = S.struct.I_D;
FVr_minbound = S.struct.FVr_minbound;
FVr_maxbound = S.struct.FVr_maxbound;
I_bnd_constr = S.struct.I_bnd_constr;
I_itermax   = S.struct.I_itermax;
F_VTR          = S.struct.F_VTR;
I_strategy     = S.struct.I_strategy;
I_refresh      = S.struct.I_refresh;
I_plotting     = S.struct.I_plotting;

% - - - - - Check input variables - - - - - - - - -

if (I_NP < 5)
  I_NP = 5;
  fprintf(1,' I_NP increased to minimal value 5\n');
end
if ((F_CR < 0) | (F_CR > 1))
  F_CR = 0.5;
  fprintf(1,'F_CR should be from interval [0,1]; set to default value 0.5\n');
end
if (I_itermax <= 0)
  I_itermax = 200;
  fprintf(1,'I_itermax should be >0; set to default value 200\n');
end
I_refresh = floor(I_refresh);

% - - - - - Check input variables - - - - - - - - -
FM_pop = zeros(I_NP,I_D); % initialize FM_pop to gain speed
% - - FM_pop is a matrix of size I_NPx(I_D+1). It will be initialized - - -
% - - - with random values between the min and max values of the - - -
% - - - - - parameters - - - - - - - - - - - - - - - -

for k=1:I_NP
  FM_pop(k,:) = FVr_minbound + rand(1,I_D) .* (FVr_maxbound - FVr_minbound);
end

FM_popold = zeros(size(FM_pop)); % toggle population
FVr_bestmem = zeros(1,I_D); % best population member ever
FVr_bestmemit = zeros(1,I_D); % best population member in iteration
I_nfeval = 0; % number of function evaluations

% ---Evaluate the best member after initialization---

I_best_index = 1;        % start with first
                         % population member
S_val(1) = feval(fname,FM_pop(I_best_index,:),S_struct);
S_bestval = S_val(1);     % best objective
                         % function value so far
I_nfeval = I_nfeval + 1;
for k=2:I_NP              % check the remaining
                           % members
    S_val(k) = feval(fname,FM_pop(k,:),S_struct);
    I_nfeval = I_nfeval + 1;
    if (left_win(S_val(k),S_bestval) == 1)
        I_best_index = k;  % save its
                           % location
        S_bestval = S_val(k);
    end
end
FVr_bestmerit = FM_pop(I_best_index,:); % best
                                        % member of current iteration
S_bestvalit = S_bestval;                 % best
                                        % value of current iteration

FVr_bestmem = FVr_bestmerit;             % best
                                        % member ever

% ----- DE-Minimization ---------------------------
% -- FM_popold is the population which has to
%    compete. It is ------
% ----- static through one iteration. FM_pop
%    is the newly ------
% ----- emerging population. --------------------
FM_pm1 = zeros(I_NP,I_D); % initialize population
                           % matrix 1
FM_pm2 = zeros(I_NP,I_D); % initialize population
                           % matrix 2
FM_pm3 = zeros(I_NP,I_D); % initialize population
                           % matrix 3
FM_pm4 = zeros(I_NP,I_D); % initialize population
                           % matrix 4
FM_pm5 = zeros(I_NP,I_D); % initialize population
```

