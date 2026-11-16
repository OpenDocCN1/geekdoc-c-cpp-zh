```
y = 0.0;
end
end
% Higher order
a = zeros(1,500);
if m >= 2 & m < 100
for k = 1:m-1
a(k) = 0.0;
x1 = x - k + 1;
if x1 >= 0.0 & x1 < 1.0
a(k) = x1;
end
if x1 >= 1.0 & x1 < 2.0
a(k) = 2 - x1;
end
end
for p=1:m-2
for q=1:m-1-p
a(q) = ((x-q+1) * a(q) + ((p+2)+q-1-x) * a(q+1)) / (p+1);
end
end
y = a(1);
end
```