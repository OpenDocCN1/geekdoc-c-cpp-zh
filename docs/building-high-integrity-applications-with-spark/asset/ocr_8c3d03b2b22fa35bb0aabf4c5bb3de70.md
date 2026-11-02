```
```ada
private
   -- Hidden details of the flight plan type
   type Flight_Plan is ...
end FMS;
```
```

Navigational databases and position determination are two of the many components making up an FMS. The client of our flight management subsystem has no need to access these two components directly. They are accessed by operations in the FMS that are called by the clients. Therefore, we place these two subsystems into private child packages. Here are the outlines of these two private children:

```
```ada
private package FMS.Navigation_Database is
   ...
end FMS.Navigation_Database;
```
```

```
```ada
private package FMS.Positioning is
   ...
end FMS.Positioning;
```
```

The body of package FMS will with these private packages to use their resources. Client units cannot with these packages.

Let us look at one more level of this FMS design. Position information is obtained through multiple subsystems including the global positioning system, inertial reference systems (IRS), and VHF omnidirectional radio range (VOR). As these three subsystems are components of the positioning system, we make them private child packages of that system.

```
```ada
private package FMS.Positioning.GPS is
   ...
end FMS.Positioning.GPS;
```
```

```
```ada
private package FMS.Positioning.IRS is
   ...
end FMS.Positioning.IRS;
```
```

```
```ada
private package FMS.Positioning.VOR is
   ...
end FMS.Positioning.VOR;
```
```

In this book we make use of private child packages in the development of hierarchical state abstractions (Sections 4.3.3 and 7.3.3), isolating non-SPARK code from legacy Ada software (Section 8.2), and partitioning unproved SPARK code (Section 9.3.5).