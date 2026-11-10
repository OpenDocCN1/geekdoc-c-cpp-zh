```
```matlab
tic;
m=4;
x5=load('heartdata00.txt'); % loading input datas from
    the file heart data.
c3=size(x5)*[1,0]; % calculating size of matrix.
u=size(x5)*[0,1];
prompt1={'Percentage of datas to be trained',
'Percentage of datas to be tested','Enter the value
of learning rate'};
dlgTitle='HEART DISEASE DIAGNOSIS USING
                    LEARNING VECTOR QUANTIZATION NETWORK';
lineNo=1;
answer1=inputdlg(prompt1,dlgTitle,lineNo);
per=str2double(answer1(1));
per1=str2double(answer1(2));
al=str2double(answer1(3));
pe=per/100;
vs=round(pe*c3);
% Seperating the input attributes and the target from the
input file for s1=1:m
    for i=1:c3
        if(x5(i,u)==(s1-1))
            for(j=1:u)
                temp=x5(s1,j);
                x5(s1,j)=x5(i,j);
                x5(i,j)=temp;
            end
        end
    end
end
for i=1:c3
    for j=1:u
        if(j==u)
            t(i)=x5(i,j);
        end
    end
end
for i=1:c3
    for j=1:u-1
        x(i,j)=x5(i,j);
    end
end
for i=1:c3
```
```