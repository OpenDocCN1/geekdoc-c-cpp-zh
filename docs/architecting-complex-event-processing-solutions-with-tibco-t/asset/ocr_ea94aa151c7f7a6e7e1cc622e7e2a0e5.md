marked as not being saved in the backing store. The configuration choices are

+   - No backing store
+   - Shared all (database) with cache-aside
+   - Shared all (database) with write-behind
+   - Shared nothing (file)

Your choice of backing store approach determines the kind of potential inconsistencies that may arise when agents are terminated unexpectedly. Because this affects the detail of design, the backing store decisions should be made before any detailed design is done.

# Claim Tracker Object Management Configuration

Table 17-1 shows the object management configuration for the Claim Tracker example. Since the Claim Tracker is not the system of record for status information (it exists to speed up the location of a claim and accelerate the identification of processing problems), fault tolerance is not a requirement and therefore there will be no replication. Due to the volume of activity, Shared-Nothing backing store is selected for efficiency. Inbound events serve only as triggers, and outbound events are not needed once sent, so all events are managed in Memory Only mode. The Claim Status and Status Report concepts are managed Cache Only.

Table 17-1: Claim Tracker Object Management Configuration

| Object | Management Mode | Replication | Backing Store |
|---|---|---|---|
| Claim Status concept | Cache Only | none | Shared Nothing |
| Status Report concept | Cache Only | none | Shared Nothing |
| Claim Status Notification event | Memory Only, ttl=0 | none | none |
| Claim Processing Exception event | Memory Only, ttl=0 | none | none |
| Claim Status Request event | Memory Only, ttl=0 | none | none |
| Claim Status Response event | Memory Only, ttl=0 | none | none |