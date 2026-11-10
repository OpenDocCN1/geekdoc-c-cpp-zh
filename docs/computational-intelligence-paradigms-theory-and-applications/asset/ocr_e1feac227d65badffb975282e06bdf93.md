# ### 15.10.1 Illustration 1: Simulation of the Movement of Swarm to Minimize the Objective Function

```
```matlab
%% Particle Swarm Optimization Simulation
% Simulates the movements of a swarm to minimize
% the objective function
% (x - 15)^2 + (y - 20)^2

% The swarm matrix is
%
% swarm(index, [location, velocity, best position,
best
% value], [x, y components or the value component])
%
%
% Initialization
% Parameters
clear
clc
iterations = 30;
inertia = 1.0;
correction.factor = 2.0;
swarm.size = 49;
% - - - - initial swarm position - - - -
index = 1;
for i = 1 : 7
    for j = 1 : 7
    swarm(index, 1, 1) = i;
    swarm(index, 1, 2) = j;
    index = index + 1;
    end
end

swarm(:, 4, 1) = 1000; % best value so far
swarm(:, 2, :) = 0;     % initial velocity
% Iterations
for iter = 1 : iterations

    %- - evaluating position & quality - - -
    for i = 1 : swarm.size
    swarm(i, 1, 1) = swarm(i, 1, 1) + swarm(i, 2, 1)/
1.3;
% update x position
```
```