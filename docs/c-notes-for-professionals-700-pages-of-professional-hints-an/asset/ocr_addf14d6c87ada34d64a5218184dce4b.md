```
```csharp
{
    public UseBulletProofing()
    {
        var ok = false;
        var result = DoSomething();
        if (!result.Contains("ERR"))
        {
            ok = true;
            DoSomethingElse();
        }
    }

    // <summary>
    // How to use Bullet Proofing in your code.
    // </summary>
    // <returns>A string</returns>
    public string DoSomething()
    {
        string result = string.Empty;
        //Note that the Bullet.Proof method forces this construct.
        Bullet.Proof(() =>
        {
            //this is the code callback
            result = "DST5900-INF-No Exceptions in this code";
        }, error =>
        {
            //error is the already logged and handled exception
            //determine the base result
            result = "DTS6200-ERR-An exception happened look at console log";
            if (error.Message.Contains("SomeMarker"))
            {
                //filter the result for Something within the exception message
                result = "DST6500-ERR-Some marker was found in the exception";
            }
        });
        return result;
    }

    // <summary>
    // Next step in workflow
    // </summary>
    public void DoSomethingElse()
    {
        //Only called if no exception was thrown before
    }
}
```
```