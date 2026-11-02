You can write SPARK code without tediously providing data and flow dependency contracts everywhere provided you are content with the synthesized contracts. This means you can “convert” existing Ada code to SPARK by just adding an appropriate SPARK_Mode aspect to an existing compilation unit as we describe in Section 7.1.1, and, of course, removing any non-SPARK constructs the unit might be using. It is not necessary to annotate all subprograms with dependency contracts before starting to work with the SPARK tools. Applying SPARK to existing Ada in this way is called *retrospective analysis*.

Earlier we emphasized that the data and flow dependency contracts are part of the specification of a subprogram. Like the parameter list, the dependency contracts should, ideally, be written as part of your design process before you have implemented the subprogram. Applying SPARK to your code base as you design and implement is called *constructive analysis*.

Yet even in the constructive case, relying on synthesized contracts is sometimes reasonable. This is particularly true for subprograms that are nested inside other subprograms or that are used only in the context of a particular package. The internal subprograms exist to service the enclosing subprogram or package and are really part of the implementation of the enclosing entity and not design elements in themselves.

The precise rules for how contracts are synthesized are detailed, but the effect is largely intuitive:

+   1. If a Global aspect exists but a Depends aspect does not the flow dependency contract is synthesized by assuming each output depends on all inputs. For small subprograms such as the Search procedure on page 105, this is often exactly correct. In any case the resulting flow dependency is conservative in the sense that it might define more dependencies than actually exist. This has the potential to increase the number of false positives in the callers but does not, for example, allow any errors such as the accidental use of uninitialized values². If false positives prove to be problematic, you can always add more precise flow dependency contracts explicitly.

+   2. If a Depends aspect exists but a Global aspect does not the data dependency contract is synthesized by examining the flow dependency contract and constructing the data dependencies from the flows. For example, suppose a subprogram is declared as follows:

```
```
procedure Do_Something(X : in Integer; Y : out Integer)
   with
      Depends => (Y => (X, A, B), B => (X, A), C => X);
```
```

This contract mentions A, B, and C, which must be visible as global variables at this point in the program. The flows specified require that A