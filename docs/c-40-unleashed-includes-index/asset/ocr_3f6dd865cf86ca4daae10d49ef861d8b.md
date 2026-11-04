public key token that will become part of the strong name of every assembly signed using the key.

![](bbox=[0.07, 0.2, 0.65, 0.55])

FIGURE 25.13 Using the Strong Name Utility sn.exe.

Using the created key.snk, we can now build and sign our calc.dll assembly as follows:

```
csc /t:library /keyfile:key.snk calc.cs
```

# Inspecting a Strong-Named Assembly

The resulting assembly manifest, shown in Figure 25.14, is much larger because it includes the public key. In addition, the hash algorithm that was used to compute the assembly's hash is revealed (SHA-1 is used by the C# compiler).

![](bbox=[0.07, 0.9, 0.62, 0.98])

FIGURE 25.14 The public key embedded in the assembly manifest.