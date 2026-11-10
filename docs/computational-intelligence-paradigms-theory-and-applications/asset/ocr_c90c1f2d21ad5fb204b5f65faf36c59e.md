```
~~~matlab
e.count=e.count+1;
e.int=i;
        % This term holds the index of the
        % last entry with a non-zero term
    end
  end
end
end

% The following if-then structure fills the vector mfc
% with the certainty of each membership function of the c
% for its current value.

  if ce.input(ii)<=cc(1)
    % Takes care of saturation of left-most mf
    mfc=[1 0 0 0 0 0 0 0 0 0 0];
    c.count=c.count+1;
    c.int=1;
  elseif ce.input(ii)>=cc(numc)
    % Takes care of saturation of the right-most mf
    mfc=[0 0 0 0 0 0 0 0 0 0 1];
    c.count=c.count+1;
    c.int=numc;
  else
    for i=1:numc
      if ce.input(ii)<=cc(i)
        mfc(i)=max([0,1+(ce.input(ii)-cc(i))/wc]);
        if mfc(i)~=0
          c.count=c.count+1;
          c.int=i; % This term holds last entry
                    % with a non-zero term
        end
      else
        mfc(i)=max([0,1+(cc(i)-ce.input(ii))/wc]);
        if mfc(i)~=0
          c.count=c.count+1;
          c.int=i; % This term holds last entry
                   % with a non-zero term
        end
      end
    end
  end
end
~~~
```