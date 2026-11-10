```
```matlab
% implemented by a digital computer.
% Hence, we sample
% the plant output every T seconds
% and at that time
% output a new value of the controller
% output.
counter=10;  % This counter will be used to count the
 % number of integration
 % steps that have been taken in the current
 % sampling interval.
 % Set it to 10 to begin so that it will
 % compute a fuzzy controller
 % output at the first step.
 % For our example, when 10 integration steps
 % have been
 % taken we will then we will sample the ship
 % heading
 % and the reference heading and compute a
 % new output
 % for the fuzzy controller.
eold=0;  % Initialize the past value of the error (for
 % use
 % in computing the change of the error, c).
 % Notice
 % that this is somewhat of an arbitrary
 % choice since
 % there is no last time step. The same
 % problem is
 % encountered in implementation.
x=[0;0;0];  % First, set the state to be a vector
x(1)=0;  % Set the initial heading to be zero
x(2)=0;  % Set the initial heading rate to be zero.
 % We would also like to set x(3) initially
 % but this
 % must be done after we have computed the
 % output
 % of the fuzzy controller. In this case,
 % by
 % choosing the reference trajectory to be
 % zero at the beginning and the other
 % initial conditions to be
 % as they are, and the fuzzy controller as
 % designed,
```
```