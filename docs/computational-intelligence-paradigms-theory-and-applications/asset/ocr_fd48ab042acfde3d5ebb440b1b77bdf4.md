```
```matlab
function f = non_domination_sort_mod(x,problem)
[N,M] = size(x);
    switch problem  case 1
        M = 2;
        V = 6;
    case 2
        M = 3;
        V = 12;
    end

front = 1;

% There is nothing to this assignment, used only to
% manipulate easily in
% MATLAB.F(front).f = [];
individual = [];
    for i = 1 : N % Number of individuals that
% dominate this individual
        % Individuals which this individual dominate
        individual(i).p = [];
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
            if dom_less == 0 & dom_equal == M
                individual(i).n = individual(i).n + 1;
            elseif dom_more == 0 & dom_equal == M
                individual(i).p = [individual(i).p j];
            end
        end
        if individual(i).n == 0
            x(i,M + V + 1) = 1;
            F(front).f = [F(front).f i];
        end
    end
```
```