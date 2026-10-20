```
ReportGenericError(e);
throw;
}
finally
{
    CleanupResources();
}
```

Different catch clauses can exist for different runtime types of exceptions. You, as an application author, must create or use different exception classes when catch clauses might take different actions. Note that every different exception above is handled in a different way. Developers only want to provide different catch clauses for different exception classes when the handling is different. Otherwise, it’s just extra work. Therefore, you should consider creating different exception classes only when you believe developers will take different actions for the problems that cause the exception. If you don’t, your users are left with only unappealing options. You can punt and terminate the application whenever an exception gets thrown. That’s certainly less work, but it won’t win kudos from users. Or, they can reach into the exception to try to determine whether the error can be corrected:

```
private static void SampleTwo()
{
    try
    {
        Foo();
        Bar();
    }
    catch (Exception e)
    {
        switch (e.TargetSite.Name)
        {
            case "Foo":
                FixProblem(e);
                break;
            case "Bar":
                ReportErrorAndContinue(e);
                break;
            // some routine called by Foo or Bar:
            default:
                ReportErrorAndShutdown(e);
```