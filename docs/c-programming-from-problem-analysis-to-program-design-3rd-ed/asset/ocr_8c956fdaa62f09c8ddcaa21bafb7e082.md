![](bbox=[0.19, 0.108, 0.252, 0.16])

A new project for the interface can be added to the solution from the **Solution Explorer** window. Right mouse click on the solution icon and then select **Add New Project**.

Intramural inherits from the **Organization** class, but does not implement the **interface**. To use the Organization component in the Intramural project, a reference had to be made to that DLL before typing the program statements.

![](bbox=[0.19, 0.249, 0.252, 0.3])

Remember that one way to add the reference is to select the project in the **Solution Explorer** window and then choose **Add Reference** from the **Project** menu bar. Because each of the components is stored as a separate project, be sure to browse the project subdirectory to locate the DLL in the bin\debug directory.

The **using OrganizationNamespace;** statement is also added to eliminate the need to fully qualify references to the **Organization** class. The source code for the **Intramural** class is shown next:

```
```csharp
// Intramural.cs
using System;

// OrganizationNamespace added to avoid fully qualifying references.
using OrganizationNamespace;

namespace IntramuralNamespace
{
    public class Intramural : Organization
    {
        private string sportType;

        public Intramural(string name, string pContact,
                          string sport)
            // Call to Organization (base) class constructor
            : base(name, pContact)
        {
            sportType = sport;
        }

        // Default constructor
        public Intramural()
        {
            sportType = "unknown";
        }
        // Property for sportType
```
```