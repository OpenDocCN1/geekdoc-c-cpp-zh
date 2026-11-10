```
```text
w=5;    % Nominal speed (in meters/sec)
u=3;    % A lower speed where the ship is more
difficult to control
abar=1; % Parameters for nonlinearity
bbar=1;

% The parameters for the tanker under ``ballast'' conditions
% (a heavy ship) are:

K.0=5.88;
tau.10=-16.91;
tau.20=0.45;
tau.30=1.43;

% The parameters for the tanker under ``full''
% conditions (a ship
% that weighs less than one under ``ballast'' conditions)
% are:

% K.0=0.83;
% tau.10=-2.88;
% tau.20=0.38;
% tau.30=1.07;

% Some other parameters are:

K=K.0*(u/ell);
tau.1=tau.10*(ell/u);
tau.2=tau.20*(ell/u);
tau.3=tau.30*(ell/u);
% Initialize parameters for the fuzzy controller

nume=11; % Number of input membership functions for the e
% universe of discourse (can change this but must
% also
% change some variables below if you make such
% a change)
numc=11; % Number of input membership functions for the c
% universe of discourse (can change this but must
% also
% change some variables below if you make such
% a change)
```
```