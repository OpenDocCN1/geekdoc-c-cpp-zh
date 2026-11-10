```
```matlab
else
    net.weightsnew.index =
                ones(1,2*net.D);
end

net.weightsnew.index =
    net.beta*(min(input,net.weights
        {new.index})) + ...
    (1-net.beta)*net.weightsnew.index;

net.labels(new.index) = input.label;
network.changed = true;
end
end % samples loop

if ~ network.changed
    fprintf(1,'Network trained in % d epochs.
                \ n',e);
    break
end
end % epochs loop
```
```

# **Observations:**

```
```text
tnet =
D : 2
max.categories : 100
vigilance : 0.7500
alpha : 1.0000e-003
epochs : 10
beta : 1
weights : [ ]
labels : [ ]
epsilon : 1.0000e-003
singlePrecision : 0
```
```

```
```text
tnet =
D : 2
max.categories : 100
vigilance : 0.7500
alpha : 1.0000e-003
epochs : 1
```
```