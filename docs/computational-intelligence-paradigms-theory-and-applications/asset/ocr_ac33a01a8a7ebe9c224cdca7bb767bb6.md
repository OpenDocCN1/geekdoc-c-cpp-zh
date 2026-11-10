```
```matlab
dept.flow = DF(i,j);
site1 = AM(ant,i);
site2 = AM(ant,j);
if site1 \textless site2
    sites.distance = DF(site1, site2);
else
    sites.distance = DF(site2, site1);
end
costs(ant) = costs(ant) + dept.flow *
sites.distance;
end
end
if (costs(ant) \textless min_cost)|(min_cost==-1)
    min_cost = costs(ant);
    ch.assign = AM(ant,:);
end
if mod(assign,100) == 0
    disp( sprintf('Assignments so far : % d
                 Cheapest cost : % d', assign,
                 min_cost));
end
assign = assign + 1;
end

end
disp( sprintf('Cheapest Cost : % d', min_cost));
disp( sprintf('Assignments : % d', assign-1));
disp(' ');
disp('Assignment');
disp('----------');
ant.index = find(costs==min(costs));
for i=1:p.size
    disp( sprintf('Dept % d to Site % d', i,
                  % ch.assign(i)));
end
```
```

**Output:** Cheapest Cost : 107
Assignments : 4945

# Assignment

+   - Dept 1 to Site 2
+   - Dept 2 to Site 1
+   - Dept 3 to Site 5
+   - Dept 4 to Site 3
+   - Dept 5 to Site 4
+   - Dept 6 to Site 8