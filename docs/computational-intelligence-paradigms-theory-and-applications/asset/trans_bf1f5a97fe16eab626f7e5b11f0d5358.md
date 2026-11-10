

```matlab
swarm(i, 1, 2) = swarm(i, 1, 2) + swarm(i, 2, 2)/1.3;
% update y position
x = swarm(i, 1, 1);
y = swarm(i, 1, 2);

val = (x - 15) ^ 2 + (y - 20) ^ 2; % fitness evaluation

if val < swarm(i, 4, 1) % if new position is better
    swarm(i, 3, 1) = swarm(i, 1, 1); % update best x,
    swarm(i, 3, 2) = swarm(i, 1, 2); % best y positions

    swarm(i, 4, 1) = val; % and best value
end
end

[temp, gbest] = min(swarm(:, 4, 1)); % global best position

%--- updating velocity vectors
for i = 1 : swarm_size
    swarm(i, 2, 1) = rand*inertia*swarm(i, 2, 1) + correction.factor*rand*(swarm(i, 3, 1) - swarm(i, 1, 1)) + correction.factor*rand*(swarm(gbest, 3, 1) - swarm(i, 1, 1)); % x velocity component
    swarm(i, 2, 2) = rand*inertia*swarm(i, 2, 2) + correction.factor*rand*(swarm(i, 3, 2) - swarm(i, 1, 2)) + correction.factor*rand*(swarm(gbest, 3, 2) - swarm(i, 1, 2)); % y velocity component
end

%% Plotting the swarm
clf
plot(swarm(:, 1, 1), swarm(:, 1, 2), 'x') % drawing swarm movements
axis([-2 30 -2 30]);
title('Swarm movements')
xlabel('Variable x')
```

![](img/d9a4cc12c48f7466f309cbd3c4549c73_699_0.png)

**图 15.2：** 群体运动——给定函数在 30 次迭代结束时达到最优值

```matlab
disp('13) Tripod');
disp(' ');
```

![](img/d9a4cc12c48f7466f309cbd3c4549c73_700_0.png)

**图 15.2：（续）**

```matlab
disp('Dynamic test functions, minima/environment evolves over time/iteration:');
disp('14 f6_bubbles_dyn');
disp('15 f6_linear_dyn');
disp('16 f6_spiral_dyn');

functchc=input('Choose test function ? ');
funcname = functnames{functchc};

disp(' ');
disp('1) Intense graphics, shows error topology and surfing particles');
disp('2) Default PSO graphing, shows error trend and particle dynamics');
disp('3) no plot, only final output shown, fastest');
plotfcn=input('Choose plotting function ? ');
if plotfcn == 1
  plotfcn = 'goplotpso4demo';
  shw = 1; % how often to update display
elseif plotfcn == 2
  plotfcn = 'goplotpso';
  shw = 1; % how often to update display
else
  plotfcn = 'goplotpso';
  shw = 0; % how often to update display
end

% set flag for 'dynamic function on', only used at very end for tracking plots
dyn_on = 0;
if functchc==14 | functchc == 15 | functchc == 16
    dyn_on = 1;
end

% xrng=input('Input search range for X, e.g. [-10,10] ? ');
% yrng=input('Input search range for Y ? ');
xrng=[-30,30];
yrng=[-40,40];
disp(' ');
% if =0 then we look for minimum, =1 then max
disp('0) Minimize')
disp('1) Maximize')
minmax=input('Choose search goal ?');
% minmax=0;
disp(' ');
mvden = input('Max velocity divisor (2 is a good choice) ? ');
disp(' ');
ps = input('How many particles (24 - 30 is common) ? ');
disp(' ');
disp('0) Common PSO - with inertia');
disp('1) Trelea model 1');
disp('2) Trelea model 2');
disp('3) Clerc Type 1 " with constriction');
modl = input('Choose PSO model ?');
% note: if errgoal=NaN then unconstrained min or max
% is performed
if minmax==1
    % errgoal=0.97643183; % max for f6 function (close enough for termination)
    errgoal=NaN;
else
    % errgoal=0;     errgoal=NaN;
end
minx = xrng(1);
maxx = xrng(2);
miny = yrng(1);
maxy = yrng(2);
%----------------------------------------------------------
dims=2;
varrange=[];
mv=[];
for i=1:dims
    varrange=[varrange;minx maxx];
    mv=[mv;(varrange(i,2)-varrange(i,1))/mvden];
end

ac = [2.1,2.1]; % acceleration constants, only used for modl=0
Iwt = [0.9,0.6]; % inertia weights, only used for modl=0
epoch = 400; % max iterations
wt_end = 100; % iterations it takes to go from Iwt(1) to Iwt(2); only for modl=0
errgrad = 1e-99; % lowest error gradient tolerance
errgraditer=100; % max # of epochs without error change >= errgrad
PSOseed = 0; % if=1 then can input particle starting positions, if=0 then all random
% starting particle positions (first 20 at zero, just for an example)
PSOseedValue = repmat([0],ps,10,1);

psoparams=...
[shw epoch ac(1) ac(2) Iwt(1) Iwt(2) wt_end errgrad errgraditer errgoal modl PSOseed];
% run pso
% vectorized version
[pso_out,t,pso_Trelea_vectorized(funcname, dims,...
mv, varrange, minmax, psoparams,plotfcn,PSOseedValue);

%------------------------------------------
% display best params, this only makes sense for static
% functions, for dynamic you’d want to see a time history
% of expected versus optimized global best values.
disp(' ');
disp(' ');
disp(['Best fit parameters: ']);
disp([' cost = ',num2str( [ input1, input2 ] )]);
disp(['------------------------------------']);
disp([' input1 = ',num2str(pso_out(1))]);
disp([' input2 = ',num2str(pso_out(2))]);
disp([' cost = ',num2str(pso_out(3))]);
disp([' mean cost = ',num2str(mean(tr))]);
disp([' # of pso = ',num2str(tr(end))]);

%% optional, save picture
% set(gcf,'InvertHardcopy','off');
% print -dmeta
% print('-djpeg','demoPSOBehavior.jpg');
```

```matlab
%----------------------------------------
% Sub Functions
%----------------------------------------
% goplotpso.m
clf
set(gcf,'Position',[651 31 626 474]); % this is the computer dependent part
% set(gcf,'Position',[743 33 853 492]);
set(gcf,'DoubleBuffer','on');

plot3(pos(:,1),pos(:,D),out,'b.','Markersize',7)
hold on
plot3(pbest(:,1),pbest(:,D),pbestval,'g.' ,'Markersize',7);
plot3(gbest(1),gbest(D),gbestval,'r.','Markersize',25);

% crosshairs
offx = max(abs(min(min(pbest(:,1)),min(pos(:,1)))),...
    abs(max(max(pbest(:,1)),max(pos(:,1)))));
offy = max(abs(min(min(pbest(:,D)),min(pos(:,D)))),...
    abs(max(max(pbest(:,D)),max(pos(:,D)))));
plot3([gbest(1)-offx;gbest(1)+offx],...
    [gbest(D);gbest(D)],...
    [gbestval;gbestval],...
    'r-.');
plot3([gbest(1);gbest(1)],...
    [gbest(D)-offy;gbest(D)+offy],...
    [gbestval;gbestval],...
    'r-.');

hold off

xlabel('Dimension 1','color','y')
ylabel(['Dimension ',num2str(D)],'color','y')
zlabel('Cost','color','y')

title('Particle Dynamics','color','w','fontweight','bold')

set(gca,'Xcolor','y')
set(gca,'Ycolor','y')
set(gca,'Zcolor','y')
set(gca,'color','k')
% camera control
view(2)
try
axis([gbest(1)-offx,gbest(1)+offx,gbest(D)-offy,gbest(D)+offy]);
catch
  axis([VR(1,1),VR(1,2),VR(D,1),VR(D,2)]);
end

% error plot, left side
subplot('position',[0.1,0.1,.475,.825]);
semilogy(tr(find(~isnan(tr))),'color','m','linewidth',2)
% plot(tr(find(~isnan(tr))),'color','m','linewidth',2)
xlabel('epoch','color','y')
ylabel('gbest val.','color','y')

if D==1
  titstr1=sprintf(['% 11.6g = % s ( | % 9.6g | )'],...
    gbestval,strrep(funcname,'_','\_'),gbest(1));
elseif D==2
  titstr1=sprintf(['% 11.6g = % s ( | % 9.6g, % 9.6g | )'],...
    gbestval,strrep(funcname,'_','\_'),gbest(1),gbest(2));
elseif D==3
  titstr1=sprintf(['% 11.6g = % s ( | % 9.6g, % 9.6g, % 9.6g | )'],...
    gbestval,strrep(funcname,'_','\_'),gbest(1),gbest(2),gbest(3));
else
  titstr1=sprintf(['% 11.6g = % s ( | % 9 inputs | )'],...
    gbestval,strrep(funcname,'_','\_'),D);
end
title(titstr1,'color','m','fontweight','bold');

grid on
% axis tight

set(gca,'Xcolor','y')
set(gca,'Ycolor','y')
set(gca,'Zcolor','y')
set(gca,'color','k')
set(gca,'YMinorGrid','off')
% text box in lower right
% doing it this way so I can format each line any way I want
subplot('position',[.62,.1,.29,.4]);
% clear titstr
if trelea==0
    PSOtype = 'Common PSO';
    xtrname = 'Inertia Weight : ';
    xtraval = num2str(wt(length(wt)));

elseif trelea==2 | trelea==1

    PSOtype = {'Trelea Type ',num2str(trelea)};
    xtrname = ' ';
    xtraval = ' ';

elseif trelea==3
    PSOtype = {'Clerc Type 1'};
    xtrname = ' chi value : ';
    xtraval = num2str(chi);

end
if isnan(errgoal)
    errgoalstr='Unconstrained';
else
    errgoalstr=num2str(errgoal);
end
if minmax==1
    minmaxstr = {'Maximize to : '};
elseif minmax==0
    minmaxstr = {'Minimize to : '};
else
    minmaxstr = {'Target to : '};
end
if rstflg==1
    rststat1 = 'Environment Change';
    rststat2 = ' ';
else
    rststat1 = ' ';
    rststat2 = ' ';
end

titstr={'PSO Model: ',PSOtype;...
 'Dimensions : ',num2str(D);...
 '# of particles : ',num2str(ps);...
 minmaxstr ,errgoalstr;...
 'Function : ',strrep(funcname,'_','\_');...
 xtrname ,xtraval;...
 rststat1 ,rststat2};

text(1,1,{titstr{1,1},titstr{1,2}},'color','g',...
'fontweight','bold');
hold on
text(1,9,{titstr{2,1},titstr{2,2}},'color','m');
text(1,8,{titstr{3,1},titstr{3,2}},'color','m');
```

