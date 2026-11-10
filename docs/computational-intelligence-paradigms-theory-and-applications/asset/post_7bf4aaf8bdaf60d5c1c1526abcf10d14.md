
### 6.12.1 MATLAB Code to Implement Fuzzy Composition

Fuzzy composition is illustrated through a MATLAB code as follows. Here the relations

R: X × Y ⟶ [0,1]

S: Y × Z ⟶ [0,1]

are denoted as R and S respectively. The composed relation T: X × Z ⟶ [0,1]

*Illustration 1:* Given R: x × y and S: y × z as follows.

R = \begin{bmatrix}0.1 & 0.3 & 0.5 & 0.6 \\ 0.3 & 0.5 & 0.8 & 1 \\ 0.2 & 0.9 & 0.7 & 0.1\end{bmatrix}

and

S = \begin{bmatrix}0 & 0.3 \\ 0.9 & 0.8 \\ 0.4 & 0.7 \\ 0.2 & 0.6\end{bmatrix}

Compute the max min composition T: x × z using a MATLAB program.

```matlab
%% Max Min Composition

R=[.1 .3 .5 .6 ; .3 .5 .8 1; .2 .9 .7 .1]
S=[0 .3;0.9 0.8;0.4 0.7; 0.2 0.6]
[x,y]=size(R);
[y1,z]=size(S);
if y==y1
T=zeros(x,z);
for i=1:x,
    for j=1:z,
        T(i,j)=max (min ([R(i,:); S(:,j)']));
    end
end
else
    display('Matrix dimension does not match')
end
```

### Observations: Max-Min composition

| Matrix | Values |
|---|---|
| R | 0.1000  0.3000  0.5000  0.6000<br>0.3000  0.5000  0.8000  1.0000<br>0.2000  0.9000  0.7000  0.1000 |
| S | 0  0.3000<br>0.9000  0.8000<br>0.4000  0.7000<br>0.2000  0.6000 |
| T | 0.4000  0.6000<br>0.5000  0.7000<br>0.9000  0.8000 |

**Illustration 2:** Given R: x × y and S: y × z as follows.

| Matrix | Values |
|---|---|
| R | 0.1  0.3  0.5  0.6<br>0.3  0.5  0.8  1<br>0.2  0.9  0.7  0.1 |
| S | 0  0.3<br>0.9  0.8<br>0.4  0.7<br>0.2  0.6 |

Compute the max product composition T: x × z using a MATLAB program.

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

### Observations: Max Product composition

R =

|  |  |  |  |
|---|---|---|---|
| 0.1000 | 0.3000 | 0.5000 | 0.6000 |
| 0.3000 | 0.5000 | 0.8000 | 1.0000 |
| 0.2000 | 0.9000 | 0.7000 | 0.1000 |

S =

|  |  |
|---|---|
| 0.0000 | 0.3000 |
| 0.9000 | 0.8000 |
| 0.4000 | 0.7000 |
| 0.2000 | 0.6000 |

T =

|  |  |
|---|---|
| 0.2700 | 0.3600 |
| 0.4500 | 0.6000 |
| 0.8100 | 0.7200 |

***Illustration 3:*** Given a fuzzy relation

|  |  |  |  |  |
|---|---|---|---|---|
| 0.1 | 0.8 | 0.5 | 0.6 | 0.7 |
| 0.8 | 1 | 0.4 | 0 | 0.2 |
| 0 | 0.1 | 1 | 0.5 | 0.2 |
| 0.7 | 0.5 | 0.2 | 1 | 0.3 |
| 0.2 | 0.9 | 0.5 | 0.3 | 1 |

Write a MATLAB program to compute R² and R³. Here we make use of the rule to compute R⁽ⁿ⁻¹⁾ = RoRoR........ R² and R³.

```matlab
% MATLAB code to compute R^2 using max min composition

R=[0.1 0.8 0.5 0.6 0.7; 0.8 1 0.4 0 0.2; 0 0.1 1 0.5 0.2; 0.7 0.5 0.2 1 0.3; 0.2 0.9 0.5 0.3 1]

[x,y]=size(R);
    R2=zeros(x,y);
    for i=1:x, % for each row of R matrix
        for j=1:y, % for each column of R matrix
            R2(i,j)=max(min([R(i,:); R(:,j)']))
        end
    end
```

### Observations: Max-Min composition

Input relation:

R =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.1000 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.4000 | 0.6000 | 0.2000 |
| 0 | 0.1000 | 1.0000 | 0.5000 | 0.2000 |
| 0.7000 | 0.5000 | 0.2000 | 1.0000 | 0.3000 |
| 0.2000 | 0.9000 | 0.5000 | 0.3000 | 1.0000 |

Output:

R2 =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.8000 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.5000 | 0.6000 | 0.7000 |
| 0.5000 | 0.5000 | 1.0000 | 0.5000 | 0.3000 |
| 0.7000 | 0.7000 | 0.5000 | 1.0000 | 0.7000 |
| 0.8000 | 0.9000 | 0.5000 | 0.5000 | 1.0000 |

```matlab
% MATLAB code to compute R^3 using max min composition
R=[0.1 0.8 0.5 0.6 0.7; 0.8 1 0.4 0.6 0.2; 0 0.1 1 0.5 0.2; 0.7 0.5 0.2 1 0.3; 0.2 0.9 0.5 0.3 1]
[x,y]=size(R);
R2=zeros(x,y);
R3=zeros(x,y);
for i=1:x, % for each row of R matrix
    for j=1:y, % for each column of R matrix
        R2(i,j)=max(min([R(i,:); R(:,j)']));
    end
end
for i=1:x, % for each row of R matrix
    for j=1:y, % for each column of R matrix
        R3(i,j)=max(min([R2(i,:); R(:,j)']));
    end
end
```

### Observations: Max-Min composition

Input relation:

R =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.1000 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.4000 | 0.6000 | 0.2000 |
| 0 | 0.1000 | 1.0000 | 0.5000 | 0.2000 |
| 0.7000 | 0.5000 | 0.2000 | 1.0000 | 0.3000 |
| 0.2000 | 0.9000 | 0.5000 | 0.3000 | 1.0000 |

Output:

R3 =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.8000 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.5000 | 0.6000 | 0.7000 |
| 0.5000 | 0.5000 | 1.0000 | 0.5000 | 0.5000 |
| 0.7000 | 0.7000 | 0.5000 | 1.0000 | 0.7000 |
| 0.8000 | 0.9000 | 0.5000 | 0.6000 | 1.0000 |

```matlab
% MATLAB code to compute R^2 using max product composition
R=[0.1 0.8 0.5 0.6 0.7; 0.8 1.0 0.4 0 0.2; 0 0.1 1.0 0.5 0.2; 0.7 0.5 0.2 1 0.3; 0.2 0.9 0.5 0.3 1]
[x,y]=size(R);
    R2=zeros(x,y);
    for i=1:x, % for each row of R matrix
        for j=1:y, % for each column of R matrix
            R2(i,j)=max(R(i,:).*R(:,j)');
        end
    end
```

### Observations: Max-Product composition

Input relation:

R =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.1000 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.4000 | 0 | 0.2000 |
| 0 | 0.1000 | 1.0000 | 0.5000 | 0.2000 |
| 0.7000 | 0.5000 | 0.2000 | 1.0000 | 0.3000 |
| 0.2000 | 0.9000 | 0.5000 | 0.3000 | 1.0000 |

Output:

R2 =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.6400 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.4000 | 0.4800 | 0.5600 |
| 0.3500 | 0.2500 | 1.0000 | 0.5000 | 0.2000 |
| 0.7000 | 0.5600 | 0.3500 | 1.0000 | 0.4900 |
| 0.7200 | 0.9000 | 0.5000 | 0.3000 | 1.0000 |

```matlab
% MATLAB code to compute R^3 using max product composition
R=[0.1 0.8 0.5 0.6 0.7; 0.8 1 0.4 0 0.2; 0 0.1 1 0.5 0.2; 0.7 0.5 0.2 1 0.3; 0.2 0.9 0.5 0.3 1]
[x,y]=size(R);
R2=zeros(x,y); R3=zeros(x,y);
for i=1:x, % for each row of R matrix
    for j=1:y, % for each column of R matrix
        R2(i,j)=max(R(i,:).*R(:,j)');
    end
end
for i=1:x, % for each row of R matrix
    for j=1:y, % for each column of R matrix
        R3(i,j)=max(R2(i,:).*R(:,j)');
    end
end
```

### Observations: Max-Product composition

Input relation:

R =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.1000 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.4000 | 0 | 0.2000 |
| 0 | 0.1000 | 1.0000 | 0.5000 | 0.2000 |
| 0.7000 | 0.5000 | 0.2000 | 1.0000 | 0.3000 |
| 0.2000 | 0.9000 | 0.5000 | 0.3000 | 1.0000 |

Output:

R3 =

|  |  |  |  |  |
|---|---|---|---|---|
| 0.6400 | 0.8000 | 0.5000 | 0.6000 | 0.7000 |
| 0.8000 | 1.0000 | 0.4000 | 0.4800 | 0.5600 |
| 0.3500 | 0.2800 | 1.0000 | 0.5000 | 0.2450 |
| 0.7000 | 0.5600 | 0.3500 | 1.0000 | 0.4900 |
| 0.7200 | 0.9000 | 0.5000 | 0.4320 | 1.0000 |

### Summary

Fuzzy Logic provides a completely different, unorthodox way to approach a problem. This method focuses on what the system should do rather than trying to understand how it works. This chapter discussed the basic fuzzy sets, operations on fuzzy sets, relations between fuzzy sets, composition and fuzzy arithmetic. A few MATLAB programs were also illustrated on topics such as membership functions, fuzzy operations, fuzzy arithmetic, relations, and composition.

### Review Questions

- 1. State “Law of excluded middle”.
- 2. Differentiate crisp and fuzzy logic.
- 3. Give a few examples of sets.
- 4. Mention a few examples of crisp and fuzzy sets.
- 5. Define universe of discourse.
- 6. What is a membership function? State the different types of membership functions.
- 7. Define Singleton and Linguistic variables.
- 8. Define term set with an example.
- 9. What are the major operations performed by a fuzzy set?
- 10. State the axioms for fuzzy complement.
- 11. State the axioms for fuzzy intersection.
- 12. State the axioms for fuzzy union.
- 13. What are aggregation operators? State the axioms for aggregation operations.
- 14. Mention the three properties to qualify a fuzzy set as a “fuzzy number”.
- 15. Explain fuzzy composition with a suitable example.

## Chapter 7: Fuzzy Inference and Expert Systems

### 7.1 Introduction

Fuzzy inference is the process of formulating the mapping from a given input to an output using fuzzy logic. The mapping then provides a basis from which decisions can be made, or patterns discerned. The process of fuzzy inference involves all the topics such as fuzzification, defuzzification, implication, and aggregation. Expert control/modeling knowledge, experience, and linking the input variables of fuzzy controllers/models to output variable (or variables) are mostly based on Fuzzy Rules. A fuzzy expert system consists of four components namely, the fuzzifier, the inference engine, and the defuzzifier, and a fuzzy rule base. This chapter focuses on these rules, expert system modeling, fuzzy controllers, and implementation of fuzzy controllers in MATLAB.

### 7.2 Fuzzy Rules

For any fuzzy logic operation, the output is obtained from the crisp input by the process of fuzzification and defuzzification. These processes involve the usage of rules, which form the basis to obtain the fuzzy output. A fuzzy if-then rule is also known as fuzzy rule, or fuzzy conditional statement or fuzzy implication. It is generally of the form

IF (x is A) AND (y is B) THEN (z is Z)

where x,y,z etc. represent the variables and A,B,Z are the linguistic values in the universe of discourse. Here the IF part is referred to as the antecedent or premise and the THEN part is referred to as consequent.
