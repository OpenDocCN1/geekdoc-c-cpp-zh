```
/// <param name="factorModifier"></param>
/// <returns></returns>
[Pure]
public int CalculatedCutFactor(int factorModifier)
{
    CutFactor = CutFactor * factorModifier;
    return CutFactor;
}
}
```

Code Listing 56: Add Pure Attribute to Method

If we had to build our project, the resulting output would indicate a successful build.

```
1>------ Rebuild All started: Project: CodeContractsDemo, Configuration:
Debug Any CPU ------
1>  elapsed time: 886,9984ms
1>  elapsed time: 177,9426ms
1>  elapsed time: 1120,0034ms
CodeContracts: CodeContractsDemo: Run static contract analysis.
1>  CodeContractsDemo -> C:\z\[]sc 2015\Code
Contracts\CodeContractsDemo\bin\Debug\CodeContractsDemo.exe
CodeContracts: CodeContractsDemo: Validated: 100,0%
CodeContracts: CodeContractsDemo: Checked 15 assertions: 13 correct (2 masked)
CodeContracts: CodeContractsDemo: Contract density: 0,98
CodeContracts: CodeContractsDemo: Total methods analyzed 6
CodeContracts: CodeContractsDemo: Methods analyzed with a faster abstract domain 0
CodeContracts: CodeContractsDemo: Methods with 0 warnings 5
CodeContracts: CodeContractsDemo: Time spent in internal, potentially costly, operations
CodeContracts: CodeContractsDemo: Overall time spent performing action #KarrPutIntoRowEchelonForm: 00:00:00.0140007 (invoked 784 times)
Overall time spent performing action #KarrIsBottom: 00:00:00.0120029 (invoked 1515 times)
Overall time spent performing action #WP: 00:00:00.2000032 (invoked 5 times)
Overall time spent performing action #CheckIfEqual: 00:00:00.0080005 (invoked 29 times)
Overall time spent performing action #ArraysAssignInParallel: 00:00:00.1430061 (invoked 1 times)
Overall time spent performing action #Simplex: 00:00:00.0810009 (invoked 19 times)
CodeContracts: CodeContractsDemo: Total time 7,821sec. 1303ms/method
CodeContracts: CodeContractsDemo: Generated 2 callee assume(s)
CodeContracts: CodeContractsDemo: Retained 0 preconditions after filtering
```