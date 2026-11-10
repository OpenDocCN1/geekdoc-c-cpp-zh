
```matlab
function f = non_domination_sort_mod(x,problem)
[N,M] = size(x);
switch problem
    case 1
        M = 2;
        V = 6;
    case 2
        M = 3;
        V = 12;
end

front = 1;

% There is nothing to this assignment, used only to
% manipulate easily in MATLAB.
F(front).f = [];
individual = [];
for i = 1 : N % Number of individuals that dominate this individual
    % Individuals which this individual dominate
    individual(i).p = [];
    individual(i).n = 0;
    for j = 1 : N
        dom_less = 0;
        dom_equal = 0;
        dom_more = 0;
        for k = 1 : M
            if (x(i,V + k) < x(j,V + k))
                dom_less = dom_less + 1;
            elseif (x(i,V + k) == x(j,V + k))
                dom_equal = dom_equal + 1;
            else
                dom_more = dom_more + 1;
            end
        end
        if dom_less == 0 & dom_equal ~= M
            individual(i).n = individual(i).n + 1;
        elseif dom_more == 0 & dom_equal ~= M
            individual(i).p = [individual(i).p j];
        end
    end
    if individual(i).n == 0
        x(i,M + V + 1) = 1;
        F(front).f = [F(front).f i];
    end
end

% Find the subsequent fronts
while ~isempty(F(front).f)
    Q = [];
    for i = 1 : length(F(front).f)
        if ~isempty(individual(F(front).f(i)).p)
            for j = 1 : length(individual(F(front).f(i)).p)
                individual(individual(F(front).f(i)).p(j)).n = ...
                    individual(individual(F(front).f(i)).p(j)).n - 1;
                if individual(individual(F(front).f(i)).p(j)).n == 0
                    x(individual(F(front).f(i)).p(j),M + V + 1) = ...
                        front + 1;
                    Q = [Q individual(F(front).f(i)).p(j)];
                end
            end
        end
    end
    front = front + 1;
    F(front).f = Q;
end
[temp,index_of_fronts] = sort(x(:,M + V + 1));
for i = 1 : length(index_of_fronts)
    sorted_based_on_front(i,:) = x(index_of_fronts(i),:);
end
current_index = 0;

% Find the crowding distance for each individual in each front
for front = 1 : (length(F) - 1)
    objective = [];
    distance = 0;
    y = [];
    previous_index = current_index + 1;
    for i = 1 : length(F(front).f)
        y(i,:) = sorted_based_on_front(current_index + i,:);
    end
    current_index = current_index + i;
    % Sort each individual based on the objective
    sorted_based_on_objective = [];
    for i = 1 : M
        [sorted_based_on_objective, index_of_objectives] = ...
            sort(y(:,V + i));
        sorted_based_on_objective = [];
        for j = 1 : length(index_of_objectives)
            sorted_based_on_objective(j,:) = ...
                y(index_of_objectives(j),:);
        end
        f_max = ...
            sorted_based_on_objective(length(index_of_objectives), V + i);
        f_min = sorted_based_on_objective(1, V + i);
        y(index_of_objectives(length(index_of_objectives)),M + V + 1 + i) = Inf;
        for j = 2 : length(index_of_objectives) - 1
            next_obj = sorted_based_on_objective(j + 1,V + i);
            previous_obj = sorted_based_on_objective(j - 1,V + i);
            if (f_max - f_min == 0)
                y(index_of_objectives(j),M + V + 1 + i) = Inf;
            else
                y(index_of_objectives(j),M + V + 1 + i) = ...
                    (next_obj - previous_obj)/(f_max - f_min);
            end
        end
    end
    distance = [];
    distance(:,1) = zeros(length(F(front).f),1);
    for i = 1 : M
        distance(:,1) = distance(:,1) + y(:,M + V + 1 + i);
    end
    y(:,M + V + 2) = distance;
    y = y(:,1 : M + V + 2);
    z(previous_index:current_index,:) = y;
end
f = z;
% End of non_domination_sort_mod

function f = selection_individuals(chromosome,pool_size,tour_size)

% function selection_individuals(chromosome,pool_size,tour_size) is the
% selection policy for selecting the individuals for the mating pool. The

max_candidate = max_candidate(1);
end
f(i,:) = chromosome(candidate(min_candidate(max_candidate)),:);
else
f(i,:) = chromosome(candidate(min_candidate(1)),:);
end
% End of selection_individuals

function f = genetic_operator(parent_chromosome,pro,mu,mum)

% This function is utilized to produce offsprings
% from parent chromosomes.
% The genetic operators crossover and mutation which
% are carried out with
% slight modifications from the original design.
% For more information read
% the document enclosed.

[N,M] = size(parent_chromosome);
switch pro
    case 1
        M = 2;
        V = 6;
    case 2
        M = 3;
        V = 12;
end
p = 1;
was_crossover = 0;
was_mutation = 0;
l_limit = 0;
u_limit = 1;
for i = 1 : N
    if rand(1) < 0.9
        child_1 = [];
        child_2 = [];
        parent_1 = round(N*rand(1));
        if parent_1 < 1
            parent_1 = 1;
        end
        parent_2 = round(N*rand(1));
        if parent_2 < 1
            parent_2 = 1;
        end
end
% Make sure that the mutation does not result in
% variables out of
% the search space. For both the MOP's the range
% for decision space
% is [0,1]. In case different variables have
% different decision
% space each variable can be assigned a range.
child_3 = parent_chromosome(parent_3,:);
for j = 1 : V
    r(j) = rand(1);
    if r(j) < 0.5
        delta(j) = (2*r(j))^(1/(mum+1)) - 1;
    else
        delta(j) = 1 - (2*(1 - r(j)))^(1/(mum+1));
    end
    child_3(j) = child_3(j) + delta(j);
    if child_3(j) > u_limit
        child_3(j) = u_limit;
    elseif child_3(j) < l_limit
        child_3(j) = l_limit;
    end
end
child_3(:,V + 1: M + V) = evaluate_objective(child_3,pro);
was_mutation = 1;
was_crossover = 0;
end
if was_crossover
    child(p,:) = child_1;
    child(p+1,:) = child_2;
    was_crossover = 0;
    p = p + 2;
elseif was_mutation
    child(p,:) = child_3(1,1 : M + V);
    was_mutation = 0;
    p = p + 1;
end
end
f = child;
% End of genetic_operator

function f = replace_chromosome(intermediate_chromosome,pro,pop)
% replace_chromosome(intermediate_chromosome,pro,pop)
% This function replaces the chromosomes based
% on rank and crowding
% distance. Initially until the population size is
% reached each front is
% added one by one until addition of a complete
% front which results in
% exceeding the population size. At this point
% the chromosomes in that
% front is added subsequently to the population
% based on crowding distance.

[N,V] = size(intermediate_chromosome);
switch pro
    case 1
        M = 2;
        V = 6;
    case 2
        M = 3;
        V = 12;
end

% Get the index for the population sort based on the rank
[temp,index] = sort(intermediate_chromosome(:,M + V + 1));

% Now sort the individuals based on the index
for i = 1 : N
    sorted_chromosome(i,:) = ...
        intermediate_chromosome(index(i),:);
end

% Find the maximum rank in the current population
max_rank = max(intermediate_chromosome(:,M + V + 1));

% Start adding each front based on rank and crowding
% distance until the
% whole population is filled.
previous_index = 0;
for i = 1 : max_rank
    current_index = max(find(sorted_chromosome(:,M + V + 1) == i));
    if current_index > pop
        remaining = pop - previous_index;
        temp_pop = ...
            sorted_chromosome(previous_index + 1 : current_index,:);
        [temp_sort,temp_sort_index] = ...
            sort(temp_pop(:, M + V + 2),'descend');
        for j = 1 : remaining
            f(previous_index + j,:) = ...
                temp_pop(temp_sort_index(j),:);
        end
        return;
    elseif current_index < pop
        f(previous_index + 1 : current_index, :) = ...
            sorted_chromosome(previous_index + 1 : current_index,:);
    else
        f(previous_index + 1 : current_index, :) = ...
            sorted_chromosome(previous_index + 1 : current_index,:);
        return;
    end
    previous_index = current_index;
end
% End of replace_chromosome

function f = evaluate_objective(x,problem)

% Function to evaluate the objective functions for the given input vector
% x. x has the decision variables

switch problem
    case 1
        f = [];
        %% Objective function one
        f(1) = 1 - exp(-4*x(1))*(sin(6*pi*x(1)))^6;
        sum = 0;
        for i = 2 : 6
            sum = sum + x(i)/4;
        end
        %% Intermediate function
        g_x = 1 + 9*(sum)^0.25;
        %% Objective function one
        f(2) = g_x*(1 - ((f(1))/(g_x))^2);
    case 2
        f = [];
        %% Intermediate function
        g_x = 0;
        for i = 3 : 12
            g_x = g_x + (x(i) - 0.5)^2;
        end
        %% Objective function one
end
```
