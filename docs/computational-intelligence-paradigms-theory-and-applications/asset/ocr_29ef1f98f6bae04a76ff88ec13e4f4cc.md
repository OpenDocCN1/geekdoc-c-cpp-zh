# Observations:

Max-Min composition

| Matrix | Values |
|---|---|
| R | 0.1000  0.3000  0.5000  0.6000<br>0.3000  0.5000  0.8000  1.0000<br>0.2000  0.9000  0.7000  0.1000 |
| S | 0  0.3000<br>0.9000  0.8000<br>0.4000  0.7000<br>0.2000  0.6000 |
| T | 0.4000  0.6000<br>0.5000  0.7000<br>0.9000  0.8000 |

**Illustration 2:** Given R: x × y and S: y₁ × z as follows.

| Matrix | Values |
|---|---|
| R | 0.1  0.3  0.5  0.6<br>0.3  0.5  0.8  1<br>0.2  0.9  0.7  0.1 |
| S | 0  0.3<br>0.9  0.8<br>0.4  0.7<br>0.2  0.6 |

Compute the max product composition T: x × y using a MATLAB program.

```
```matlab
% Max Product composition
R=[.1 .3 .5 .6; .3 .5 .8 1; .2 .9 .7 .1]
S=[0 .3;0.9 0.8;0.4 0.7; 0.2 0.6]
[x,y]=size(R);
[y1,z]=size(S);
if y==y1
T=zeros(x,z);
for i=1:x,
for j=1:z,
T(i,j)=max(R(i,:).*S(:,j)');
end
end
else
display('Matrix dimension does not match')
end
```
```