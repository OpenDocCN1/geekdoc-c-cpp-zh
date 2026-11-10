# 12.3 Illustration 3: Maximizing the Given
One-Dimensional Function with the Bound-
aries
Using Evolutionary Algorithm

```
%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% Main Program

%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% boundaries
bounds = [-10 10];
% pop size
n = 10;
% number of iterations
numits = 100;
% number of mutations per it
nummut = 1;

f = @multipeak;

blength = bounds(2)-bounds(1);

% initial population

pop = rand(1,n) * blength + bounds(1);

for it=1:numits
    % fitness eval
    for i=1:n, fpop(i) = feval(f, pop(i)); end
    maxfit = max(fpop);
    meanfit = mean(fpop);
    % subtract lowest fitness in order to normalize
    m=min(fpop);
    fpop=fpop-m;
    cpop(1) = fpop(1);
    for i=2:n, cpop(i) = cpop(i-1) + fpop(i); end

    % SELECTION
    totalfitness = cpop(n);
```