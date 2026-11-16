```
x=conv(x,g0)+conv(y,g1);
C(k,:)=rot90(x(4:length(x)-4));
end
s=C;
clear C
for k=1:132
x=zeros(136,1);
x(1:2:136)=s(1:68,k);
y=zeros(136,1);
y(1:2:136)=s(69:136,k);
x=conv(x,g0)+conv(y,g1);
C(:,k)=x(4:length(x)-4);
end
LL_rec=C;
clear C
% First level reconstruction
s=[LL_rec LH; HL HH];
for k=1:264
x=zeros(264,1);
x(1:2:264)=rot90(s(k,1:132),3);
y=zeros(264,1);
y(1:2:264)=rot90(s(k,133:264),3);
x=conv(x,g0)+conv(y,g1).
```