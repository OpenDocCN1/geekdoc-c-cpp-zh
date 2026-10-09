# Code Listing 7: The TwilioCore Class with the RegisterUser Method

```
using System;
using Authy.Net;

namespace TwilioSuccinctly
{
    public class TwilioCore : IDisposable
    {
        protected bool disposed;

        public TwilioCore()
        {
        }

        ~TwilioCore()
        {
            Dispose(false);
        }

        public virtual void Dispose(bool disposing)
        {
            if (!disposed)
            {
                if (disposing)
                {
                }

                disposed = true;
            }
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        public RegisterUserResult RegisterUser(string apikey, string
                                               uemail, string unumber, int cc, bool tmode)
        {
            if (apikey != string.Empty && uemail != string.Empty &&
                unumber != string.Empty)
            {
                AuthyClient client = new AuthyClient(apikey, tmode);
                return client.RegisterUser(uemail, unumber, cc);
            }
            else
```