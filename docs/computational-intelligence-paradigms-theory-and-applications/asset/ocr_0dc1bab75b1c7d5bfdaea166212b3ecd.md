```
```matlab
% Collect the '+ parts'
[vv,fs,vvdel] = fsgen(tree,symbols);
if ~isempty(vvdel),
    error('Fatal error: redundant strings after
        deleting');
end

% OLSQ
[vfsdel,err] = gpols_olsq(fs,X,Y,olslimit);
tree.err = err;
vvdel = vv(vfsdel);

% Prune redundant parts
tree = prunetree(vvdel,tree,symbols);

% Collect the '+ parts'
[vv,fs,vvdel] = fsgen(tree,symbols);
if ~isempty(vvdel),
    error('Fatal error: redundant strings after
        deleting');
end

% LSQ
[mse,cfsq,theta] = gpols.lsq(fs,X,Y);
fit = cfsq;

% Tree-size penalty
if a1~=0 & a2~=0,
    Sl = treesize(tree);
    fit = fit ./ (1+exp(a1*(Sl-a2)));
end

% Chrom
popu.chromj.tree = tree; % write back the tree
popu.chromj.mse = mse;
popu.chromj.fitness = fit;
popu.chromj.tree.param(1:length(theta)) = theta;
popu.chromj.tree.paramm = length(theta);

end

%--------------------------------------------------------------
function [tree] = polytree(treein);
tree = treein;
v = [];
vv = [];
i = 1;
```
```