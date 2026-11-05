```
```csharp
// FratSorority.cs
using System;
using OrganizationNamespace;
using IFundingNamespace;

namespace FratSororityNamespace
{
    public class FratSorority : Organization, IFunding
    {
        private bool chartered; // Private member data
        private string houseAddress;

        public FratSorority()
        {
            houseAddress = "unknown";
            chartered = false;
        }

        public FratSorority(string name, string pContact,
                            bool isChartered, string address)
            : base(name, pContact)
        {
            // Call to base constructor
            houseAddress = address;
            chartered = isChartered;
        }

        // Required method - because of interface
        public void SetFundingAmt()
        {
            if(chartered)
            {
                FundedAmt = 500M;
            }
            else
            {
                FundedAmt = 0M;
            }
        }

        // Properties
        private bool Chartered
        {
            get
            {
                return chartered;
            }
            set
            {
                chartered = value;
            }
        }
    }
}
```
```