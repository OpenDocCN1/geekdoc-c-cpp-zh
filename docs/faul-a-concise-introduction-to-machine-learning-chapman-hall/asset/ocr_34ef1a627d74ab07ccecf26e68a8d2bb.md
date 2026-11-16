```
```matlab
load fisheriris

% Extract two attributes.
pl = meas(:,3); % petal length
pw = meas(:,4); % petal width
X = [pl pw];

% Create classifier.
k = 5
knnModel = fitcknn(X,species,...
    'NumNeighbors',k,...
    'Standardize',true); % standardize data

% Lay grid over the region.
d = 0.01;
[x1Grid,x2Grid] = meshgrid(0:d:7,0:d:3);
XGrid = [x1Grid(:),x2Grid(:)];
N = size(XGrid,1);

% For each grid point calculate the score of each class.
% 'predict' returns the predicted class labels corresponding to the
% minimum misclassification cost, the score (posterior probability)
% and the cost of the expected misclassification cost for
% each class.
[~,score,~] = predict(knnModel,XGrid);

% Classify according to the maximum score.
[~,maxScore] = max(score,[],2);

% Plot classifier regions.
figure
h(1:5) = gscatter(xGrid(:,1),xGrid(:,2),maxScore,...
    [0.5 0.5 0.5; 0.7 0.7 0.7; 0.9 0.9 0.9]);
hold on

% Plot data.
h(4:6) = gscatter(pw, pl, species,'rgb','o*^');
xlabel('Petal length');
ylabel('Petal width');
legend(h,{'Setosa region','Versicolor region','Virginica region',...
    'Setosa','Versicolor','Virginica'},...
    'Location','Northwest');
axis([0.8 7.0 0 3])

% Plot new points with ellipses containing nearest neighbours.
newpoints = [2.5 .75;...
    5 2;...
    2 1.4];
plot(newpoints(:,1),newpoints(:,2),'xk','linewidth',1.5);

% Find nearest neighbours.
[idx,d] = knnsearch(X,newpoints,...
    'K',k,...
    'Distance','seuclidean'); % Euclidean distance on standardized data

% Mark neighbours.
plot(newpoints(idx,2),ok,'markersize',10);

% Plot ellipses.
for i=1:3
    a = knnModel.Sigma < -d(i,end) % scale standardized coordinates
    newpoints(i,:) = a % corner of rectangle containing ellipse
    % Draw an ellipse around the nearest neighbours.
    h = rectangle('position',[c,x2s(1),x2s(2),...
        'curvature',[1 1],'LineStyle','--');
end
hold off
```
```

# Listing 5.3: k Nearest Neighbours.