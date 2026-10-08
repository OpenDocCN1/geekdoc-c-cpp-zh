```
float diameter;
float length;
float load;
float stress;
};
```

```
typedef struct forces FORCES;

int main()
{
    const float PI = 3.141593;
    FORCES compforce;
    float area;
```

```
scanf("%4c %14c", compforce.type.loadtype,
    compforce.type.materials);
scanf("%f %f %f", &compforce.diameter,
    &compforce.length,&compforce.load);
```

```
compforce.type.loadtype[4] = '\0';
compforce.type.materials[14] = '\0';

```

```
area = ( PI * compforce.diameter
    compforce.diameter) / 4.0;
```

```
compforce.stress = compforce.load / area;
```

```
printf("%s %s %5.2f %5.2f %10.2f %10.2f",
compforce.type.loadtype,compforce.type.materials,
compforce.diameter,compforce.length,compforce.load,
compforce.stress);
```

```
return 0;
}
```

In this code type is a member of struct forces where type is a structure variable
of the data type LOAD. To access a member of the LOAD variable type from the vari-
ables of the type FORCES, the member operator must be used twice as shown in the
code. For example, to access the member materials of the member structure LOAD
of the FORCES variable compforce, you must first access the structure member type
 then access the structure member materials using the member operator twice
as follows: compforce.type.materials. Similarly the tensile forces and shear
forces may be implemented.