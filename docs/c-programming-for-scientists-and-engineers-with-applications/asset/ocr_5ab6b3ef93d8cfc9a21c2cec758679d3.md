# 11.5 Union and Enumeration Data Types

number of bytes required for a data member declared in the union. In this case the member balance is allocated eight bytes of storage because its data type is double.

In engineering and scientific applications arrays are very common data structures. Unions are very useful for solving problems with large arrays when storage optimization is required. The following example of a union and union variable shows such an application.

union fluid
{}

```
float pressure[100] [200];nfloat velocity[100] [200];nfloat density[1000] [200];
}
```

The declaration of union variables as arrays;

union fluid airflow[500];

Notice that the members of the union pressure is an array of 100 rows and 200 columns, which is 20,000 elements, the array velocity is an array of 100 rows and 200 columns, which is 20,000 elements, and density is an array of 100 rows and 200 columns, which is 20,000 elements. The union member pressure array, which is a member of the union variable airflow[0], is assigned a value of 230 psi for the first row as follows:

```
airflow[0].pressure[0] [0] = 230;
airflow[0].pressure[0] [1] = 230;
```

```
airflow[0].pressure[0] [199] = 230;
```

Notice that the storage is used only for the member pressure of the union elements airflow[0] through airflow[99].

Now if values are assigned to the union airflow[0].velocity[0] [0], velocity[0][1], ..., velocity-ity[0] [199], and so on. Then the values for the union member pressure will not exist and so on. Then the values for the union member pressure will not exist. The maximum storage is used for the union member density because it has 200,000 elements and it requires a storage for all the elements of the union variable airflow[500], which is 1 million locations of four bytes each. When the storage is used for the member density the values stored previously for the members pressure and velocity no longer exist.