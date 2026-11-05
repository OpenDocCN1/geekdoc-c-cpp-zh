- If the PNRP ID is not found and there is no PNRP ID in its cache that is closer to the target PNRP ID, the requested peer sends the requesting peer a response that indicates this condition. The requesting peer then chooses the next-closest PNRP ID.

- **The requesting peer continues this process with successive iterations, eventually locating the node that registered the PNRP ID.**

- In PNRP, to resolve a Peer Name, the Peer Name, search criteria and optional cloud name (Global by default) and IP address hint is to be provided. Typically, a lookup is used to determine if a Peername already exists or to contact it directly. The following search criteria options are supported,

| Default | Uses the NonCurrentProcessPeerName option |
|---|---|
| **AnyPeerName** | The matching peer name can be registered locally or remotely. |
| **NearestNonCurrentProcessName** | The matching peer name can be registered locally or remotely, but the resolve request excludes any peer name registered by the process making the resolve request and looks for the service closest to the local IP address. |
| **NearestPeerName** | The matching peer name can be registered locally or remotely, but the resolve request looks for the service closest to the local IP address. |
| **NearestRemotePeerName** | The resolve request excludes any peer name registered locally on this computer and looks for the service closest to the local IP address. |
| **NonCurrentProcessPeerName** | The matching peer name can be registered locally or remotely, but the resolve request excludes any peer name registered by the process making the resolve request. |
| **RemotePeerName** | The resolve request excludes any peer name registered locally on this computer. |