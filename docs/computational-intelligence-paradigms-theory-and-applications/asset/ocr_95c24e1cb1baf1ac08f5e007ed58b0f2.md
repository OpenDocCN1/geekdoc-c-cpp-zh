```
```matlab
X = X([1 2 3 4 5],:);
numPatterns = size(X,1);
numInputs = size(X,2);
% Plot the fundamental memories.
figure
plotHopfieldData(X)

% STEP 1. Calculate the weight matrix using Hebb's
postulate
W = (X' * X- numPatterns)*eye(numInputs)/numInputs;

% STEP 2. Set a probe vector using a predefined
noiselevel. The probe
% vector is a distortion of one of the fundamental
memories
noiseLevel = 1/3;
patInd = ceil(numPatterns*rand(1,1));
xold =
(2*(rand(numInputs,1)>noiseLevel)-1).*X(patInd,:)';

% STEP 3. Asynchronous updates of the elements of the
% probe vector until it converges. To guarantee convergence,
% the algorithm performs at least numPatterns=81 iterations
% even though convergence generally occurs before this
figure
converged = 0;
x=xold;
while converged==0,
        p=randperm(numInputs);
        for n=1:numInputs
            r = x(p(n));
            x(p(n)) = hsign(W(p(n),:)*x, r);
            plotHopfieldVector(x);
            pause(0.01);
        end

% STEP 4. Check for convergence
                if (all(x==xold))
                    break;
                end
                xold = x;
end
```
```