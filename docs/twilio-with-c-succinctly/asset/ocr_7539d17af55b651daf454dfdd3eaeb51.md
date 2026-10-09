```
public bool FollowedUp { get; set; }
public string PhoneNumber { get; set; }
}

public class LeadsCore : IDisposable
{
    private const string cStrConnStr = 
        "<< Your Azure Storage Connection String >>";
    private const string cStrAppTable = "LeadsSuccinctly";

    protected bool disposed;

    public LeadsData Data { get; set; }

    public LeadsCore()
    {
        LeadsData ld = new LeadsData();
        
        ld.FullName = string.Empty;
        ld.Email = string.Empty;
        ld.Webinar = string.Empty;
        ld.PhoneNumber = string.Empty;
    }

    ~LeadsCore()
    {
        Dispose(false);
    }

    public virtual void Dispose(bool disposing)
    {
        if (!disposed)
        {
            if (disposing)
            { }
            
            Data = null;
        }
        disposed = true;
    }

    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }
}
```