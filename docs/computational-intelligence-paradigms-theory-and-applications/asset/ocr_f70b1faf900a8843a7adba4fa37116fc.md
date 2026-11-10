```
```matlab
Kdmin=-500;
Kdmax=-0; % Program below assumes this

KpKd=0*ones(2,S,Nevsteps);
for ss=1:S
    KpKd(1,ss,1)=Kpmin+rand; % Generates a random
                              % proportional gain in range
    KpKd(2,ss,1)=Kdmin+rand; % Generates a random
                              % proportional gain in range
end

% Store performance measure for evaluating closed
  ~loop performance

Jcl=0*ones(S,Nevsteps); % Allocate memory

% Define scale parameters for performance measure
w1=1;
w2=0.01;

% Set parameters that determine size of cloud of
  design points about best one

beta1=0.5;
beta2=50;

% Set the probability that a mutation will occur
(only one can mutate per $ generation as is)
pm=1;

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
% Start evolutionary design loop

for k=1:Nevsteps+1
    % Loop for evolution (note that add one
    % simply to show the best controller up to
    % the last one and so that 0 in the plots
    % corresponds to the initial condition)
    for ss=1:S
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

% Simulate the controller regulating the ship heading
```
```