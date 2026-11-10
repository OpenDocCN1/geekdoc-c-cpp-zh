
![](img/d9a4cc12c48f7466f309cbd3c4549c73_548_0.png)

**FIGURE 12.3:** Plot of the Error between Ship Heading and Reference Model Heading

plotted in Figure 12.3. The closed loop performance measure, proportional gain, and the derivative gain are plotted in Figures 12.4, 12.5 and 12.6 respectively.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_548_1.png)

**FIGURE 12.4:** Performance Measure for the Best Controller

![](img/d9a4cc12c48f7466f309cbd3c4549c73_549_0.png)

**FIGURE 12.5:** Proportional Gain

![](img/d9a4cc12c48f7466f309cbd3c4549c73_549_1.png)

**FIGURE 12.6:** Derivative Gain

## 12.3 Illustration 3: Maximizing the Given One-Dimensional Function with the Boundaries Using Evolutionary Algorithm

```matlab
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
    maxf(it) = max(fpop);
    meanf(it) = mean(fpop);
    % subtract lowest fitness in order to normalize
    m=min(fpop);
    fpop=fpop-m;
    cpop(1) = fpop(1);
    for i=2:n, cpop(i) = cpop(i-1) + fpop(i); end

    % SELECTION
    totalfitness = cpop(n);

    % use roulette selection (-> need pos. fitness!)
    for i=1:n
        p=rand*totalfitness;
        % now find first index
        j=find(cpop-p>0);
        if isempty(j)
            j=n;
        else
            j=j(1);
        end
        parent(i)=pop(j);
    end
    % pop, fpop, parent, pause
    % REPRODUCTION
    % parents 2i-1 and 2i make two new children 2i-1
    % and 2i
    % crossover

    % use arithmetic crossover
    for i=1:2:n
        r=rand;
        pop(i)   = r*parent(i)   + (1-r)*parent(i+1);
        pop(i+1) = (1-r)*parent(i) + r*parent(i+1);
    end

    % mutation
    % use uniform mutation
    for i=1:nummut
        pop(ceil(rand*n)) = bounds(1) + rand*blength;
    end
end
pop
for i=1:n, fpop(i) = feval(f, pop(i)); end
fpop

close all
ezplot(@multipeak,[-10 10])
hold on
[y,xind]=max(fpop);
plot(pop(xind),y,'ro')
title('Multipeak at (6.4488,44.3352)')
xlabel('Population')
ylabel('Variable y')

figure, plot(maxf), hold on, plot(meanf,'r-');
title('Maximum and Mean of the 1-D function');
xlabel('Population')
ylabel('Variable y')
%%%%%%%%%%%%%%%% End of Main %%%%%%%%%%%%%%%%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Subprogram used
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
function y = multipeak(x)
% Demonstration evaluation function
% f(x)=x+10sin(5x)+7cos(4x) + 25

y = x + 10*sin(5*x)+7*cos(4*x) + 25;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

### Observations

Figure 12.7 shows the multi-peak of the given function which occurs at (6.4488, 44.3352) and Figure 12.8 shows the maximum and mean value of the given function.

![](img/d9a4cc12c48f7466f309cbd3c4549c73_552_0.png)

**FIGURE 12.7:** Multi-Peak for the Given Function

![](img/d9a4cc12c48f7466f309cbd3c4549c73_553_0.png)

**FIGURE 12.8:** Maximum and Mean of the Given Function

## 12.4 Illustration 4: Multiobjective Optimization Using Evolutionary Algorithm (MOEA)

This problem is to find the global optimal space solution for a discontinuous function given by

$$f_1(x) = 1 - e^{-4x_1} \sin^6(6\pi x_1)$$

$$f_2(x) = g(x)\left(1 - \left(\frac{f_1(x)}{g(x)}\right)^2\right)$$

where \(g(x) = 1 + 9\left(\sum_{i=1}^6 \frac{x_i}{4}\right)^{0.25}\) subject to \(0 \le x_i \le 1\)

```matlab
% Main program to run the MOEA

%% Initialize the variables
% Declare the variables and initialize their values
% pop - population
% gen - generations
% pro - problem number
pop = 200;
gen = 1000;
pro = 1;

switch pro
    case 1
        % M is the number of objectives.
        M = 2;
        % V is the number of decision variables.
        % In this case it is
        % difficult to visualize the decision
        % variables space while the
        % objective space is just two dimensional.
        V = 6;
    case 2
        M = 3;
        V = 12;
end

% Initialize the population
chromosome = initialize_variables(pop,pro);
%% Sort the initialized population
% Sort the population using non-domination-sort. This returns two columns
% for each individual which are the rank and the
% crowding distance
% corresponding to their position in the front they belong.
chromosome = non_domination_sort_mod(chromosome,pro);
%% Start the evolution process
% The following are performed in each generation
% Select the parents
% Perform crossover and Mutation operator
% Perform Selection.
for i = 1 : gen
    % Select the parents
    % Parents are selected for reproduction to generate offspring by
    % tournament selection The arguments are
    % pool - size of the mating pool. It is common to have this to be half
    % the population size.
    % tour - Tournament size.
    pool = round(pop/2);
    tour = 2;

    parent_chromosome = tournament_selection(chromosome,pool,tour);
    % Perform crossover and Mutation operator
    % Crossover probability pc = 0.9 and mutation
    % probability is pm = 1/n, where n is the number
    % of decision variables.
    % Both real-coded GA and binary-coded GA are
    % implemented in the original
    % algorithm, while in this program only the
    % real-coded GA is considered.
    % The distribution indices for crossover and
    % mutation operators
    % as mu = 20
    % and mum = 20 respectively.
    mu = 20;
    mum = 20;
    offspring_chromosome = genetic_operator(parent_chromosome,pro,mu,mum);

    % Intermediate population
    % Intermediate population is the combined population of parents and
    % offsprings of the current generation.
    % The population size is almost 1 and
    % half times the initial population.
    [main_pop,temp] = size(chromosome);
    [offspring_pop,temp] = size(offspring_chromosome);
    intermediate_chromosome(main_pop + 1 : main_pop + offspring_pop,1 : M + V) = ...
        offspring_chromosome;

    % Non-domination-sort of intermediate population
    % The intermediate population is sorted again based on non-domination sort
    % before the replacement operator is performed on the intermediate
    % population.
    intermediate_chromosome = ...
        non_domination_sort_mod(intermediate_chromosome,pro);
    % Perform Selection
    % Once the intermediate population is sorted only the best solution is
    % selected based on it rank and crowding distance. Each front is filled in
    % ascending order until the addition of population size is reached. The
    % last front is included in the population based on the individuals with
    % least crowding distance
    chromosome = replace_chromosome(intermediate_chromosome,pro,pop);
    if mod(i,10) == 0
        fprintf('%8d\n',i);
    end
end

%% Result
% Save the result in ASCII text format.
save solution.txt chromosome -ASCII

%% Visualize
% The following is used to visualize the result for the given problem.
switch pro
    case 1
        plot(chromosome(:,V + 1),chromosome(:,V + 2),'*');
        xlabel('f(x_1)');
        ylabel('f(x_2)');
    case 2
        plot3(chromosome(:,V + 1),chromosome(:,V + 2),chromosome(:,V + 3),'*');
        xlabel('f(x_1)');
        ylabel('f(x_2)');
        zlabel('f(x_3)');
end

%%%%%%%% End of Main Program %%%%%%%%

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Subprograms
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

function f = initialize_variables(N,problem)
% function f = initialize_variables(N,problem)
% N - Population size
% problem - takes integer values 1 and 2 where,
% '1' for MOP1
% '2' for MOP2
%
% This function initializes the population with N
% individuals and each individual having M decision variables based on
% the selected problem.
% M == 6 for problem MOP1 and M == 12 for problem MOP2.
% The objective space
% for MOP1 is 2 dimensional while for MOP2 is 3
% dimensional.
% Both the MOP's has 0 to 1 as their range for all the
% decision variables.
min = 0;
max = 1;
switch problem
    case 1
        M = 6;
        K = 8;
    case 2
        M = 12;
        K = 15;
end
for i = 1 : N
    % Initialize the decision variables
    for j = 1 : M
        f(i,j) = rand(1); % i.e f(i,j) = min + (max - min)*rand(1);
    end
    % Evaluate the objective function
    f(i,M + 1: K) = evaluate_objective(f(i,:),problem);
end

%%%%%% End of initialize_variables %%%%%%%%
%%% Non-Domination Sort

% This function sort the current population based on
% non-domination. All the individuals in the first front are given a rank of
% 1, the second front
% individuals are assigned rank 2 and so on. After
% assigning the rank the
% crowding in each front is calculated.
```
