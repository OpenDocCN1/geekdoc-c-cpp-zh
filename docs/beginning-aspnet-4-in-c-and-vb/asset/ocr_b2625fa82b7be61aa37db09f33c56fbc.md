```
```csharp
[OperationContract]
RoomReservation[] GetRoomReservations(DateTime fromDate, DateTime toDate);
}
```
```

*code snippet RoomReservationService/IRoomService.cs*

# Service Implementation

The service class RoomReservationService implements the interface IRoomService. The service is implemented just by invoking the appropriate methods of the RoomReservationData class:

```
```csharp
using System;
using System.Linq;

namespace Wrox.ProcSharp.WCF
{
    public class RoomReservationService : IRoomService
    {
        public bool ReserveRoom(RoomReservation roomReservation)
        {
            var data = new RoomReservationData();
            data.ReserveRoom(roomReservation);
            return true;
        }

        public RoomReservation[] GetRoomReservations(DateTime fromDate, DateTime toDate)
        {
            var data = new RoomReservationData();
            return data.GetReservations(fromDate, toDate);
        }
    }
}
```
```

*code snippet RoomReservationService/RoomReservationService.cs*

# WCF Service Host and WCF Test Client

The WCF Service Library project template creates an application configuration file named App.config that you need to adapt to the new class and interface names. The service element references the service type RoomReservationService, including the namespace; the contract interface needs to be defined with the endpoint element.

```
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <system.web>
        <compilation debug="true" />
    </system.web>
    <!-- When deploying the service library project, the content of the config file must be added to the host's app.config file. System.Configuration does not support config files for libraries. -->
    <system.serviceModel>
        <services>
            <service name="Wrox.ProcSharp.WCF.RoomReservationService">
                <host>
                    <baseAddresses>
                        <add baseAddress = "http://localhost:8732/Design_Time_Addresses/RoomReservationService/Service1/" />
```
```