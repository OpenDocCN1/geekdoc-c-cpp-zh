```
% for its current value (to understand this part of the
% code see the above similar code for computing mfc).
% Clearly, it could be more efficient to make a subroutine
% that performs these computations for each of the fuzzy
% system inputs.

if c(index)<=cc(1)
    % Takes care of saturation of left-most mf
    mfc=[1 0 0 0 0 0 0 0 0 0];
    c_count=c_count+1;
    c_int=1;
elseif c(index)>=cc(numc)
    % Takes care of saturation of the right-most mf
    mfc=[0 0 0 0 0 0 0 0 0 1];
    c_count=c_count+1;
    c_int=numc;
else
    for i=1:numc
        if c(index)<=cc(i)
            mfc(i)=max([0,1+(c(index)-cc(i))/wc]);
            if mfc(i)~=0
                c_count=c_count+1;
                c_int=i;
            % This term holds last entry
                % with a non-zero term
            end
        end
    end
end

% The next two loops calculate the crisp output using
% only the non- zero premise of error,e, and c. This
% cuts down computation time since we will only compute
% the contribution from the rules that are on (i.e., a
% maximum of four rules for our case). The minimum
% is center-of-gravity used for the premise
% (and implication for the defuzzification case).

num=0;
den=0;
for k=e_int-e_count+1:e_int
    % Scan over e indices of mfs that are on
    for l=c_int-c_count+1:c_int
```