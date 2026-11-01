# TRY IT OUT  WCF Contracts: Ch22Ex02Contracts

1. Create a new WCF Service Application project called Ch22Ex02 in the directory C:\BegVCSharp\Chapter22.

2. Add a class library project called Ch22Ex02Contracts to the solution and remove the Class1.cs file.

3. Add references to the System.Runtime.Serialization.dll and System.ServiceModel.dll assemblies to the Ch22Ex02Contracts project.

4. Add a class called Person to the Ch22Ex02Contracts project and modify the code in Person.cs as follows:

```
```csharp
using System.Runtime.Serialization;
namespace Ch22Ex02Contracts
{
    [DataContract]
    public class Person
    {
        [DataMember]
        public string Name { get; set; }
        [DataMember]
        public int Mark { get; set; }
    }
}
```
```

5. Add an interface called IAwardService to the Ch22Ex02Contracts project and modify the code in IAwardService.cs as follows:

```
```csharp
using System.ServiceModel;
namespace Ch22Ex02Contracts
{
    [ServiceContract(SessionMode = SessionMode.Required)]
    public interface IAwardService
    {
        [OperationContract(IsOneWay = true, IsInitiating = true)]
        void SetPassMark(int passMark);
        [OperationContract]
        Person[] GetAwardedPeople(Person[] peopleToTest);
    }
}
```
```

6. In the Ch22Ex02 project, add a reference to the Ch22Ex02Contracts project.

7. Remove IService1.cs and Service1.svc from the Ch22Ex02 project.

8. Add a new WCF service called AwardService to Ch22Ex02.

9. Remove the IAwardService.cs file from the Ch22Ex02 project.

10. Modify the code in AwardService.svc.cs as follows:

```
```csharp
using System.Collections.Generic;
using Ch22Ex02Contracts;
namespace Ch22Ex02
{
    public class AwardService : IAwardService
```
```