```
```matlab
% Set eta
eta = 0.05/numPatterns;
for i=1:numEpochs
                % Calculate outputs, errors, and gradients
                phi = [ones(size(X,1),1) tanh(X*Wh)];
                y = phi*wo;
                err = y-t;
                go = phi'*err;
                Gh = X'*((1-phi(:,2:numHidden+1)).^2 ...
                    (err*wo(2:numHidden+1)'));
                % Perform gradient descent.
                wo = wo - eta*go;
                Wh = Wh - eta*Gh;
                % Update performance statistics.
                mse(i) = var(err);
end

plot(1:numEpochs, mse, '-r')
hold on
end

fsize=15;
set(gca,'xtick',[0:500:2000],'FontSize',fsize)
set(gca,'ytick',[0:0.5:1],'FontSize',fsize)
xlabel('Number of Epochs','FontSize',fsize)
ylabel('Mean Squared Error','FontSize',fsize)
hold off

% --------------------------
% End of Main
% --------------------------
```
```

# Observations

The performance statistics of the generalized delta learning rule and backpropagation of errors for a multilayer network is shown in Figure 5.11. It is found that the Mean Squared Error decreases as the number of epochs increases.