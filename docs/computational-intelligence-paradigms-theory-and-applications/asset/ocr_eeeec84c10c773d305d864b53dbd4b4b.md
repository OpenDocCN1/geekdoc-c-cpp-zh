```
~~~matlab
% INP number of population members
    INP = 15; % pretty high number -
      needed for demo purposes only

% Itermax maximum number of iterations(generations)
    Itermax = 50;

% F_weight DE-stepsize F_weight ex [0, 2]
    F_weight = 0.85;

% F_CR crossover probability constant ex [0, 1]
    F_CR = 1;

% Lstrategy 1 -->DE/rand/1:
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

Lstrategy = 3

% I_refresh intermediate output will be produced after
%       "I_refresh" iterations. No intermediate
%       output will be produced if I_refresh is <1
I_refresh = 1;

% I_plotting    Will use plotting if set to 1. Will
% skip plotting otherwise.
I_plotting = 1;

%--Problem dependent constant values for plotting--
~~~
```