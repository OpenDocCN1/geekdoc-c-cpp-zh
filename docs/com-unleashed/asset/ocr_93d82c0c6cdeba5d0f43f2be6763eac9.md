# TABLE 21.4 The Scenario Fields

| Field Name | Type | Description |
|---|---|---|
| ScenarioID | Int | A unique identifier for a test. |
| TestName | Varchar(120) | The name of the test. |
| TotalDatabaseNodes | Int | The total number of database nodes to be used in the test. |
| DriversPerDatabaseNode | Int | The number of Drivers used per database node. The total number of drivers is this number times TotalDatabaseNodes. |
| DriverType | Int | A number to indicate what type of driver to use. For example, a 1 indicates a COM driver, whereas a 2 indicates a Web driver. |
| ClientsPerDriver | Int | The number of clients used for each driver node. The total number of clients for a test is TotalDatabaseNodes× DriversPerDatabaseNode×ClientsPerDriver. This value only applies to the COM driver. |
| ConnectionsPerDriver | Int | The number of connections to use for the Web driver. |
| NumberOfConfigs | Int | The number of configurations from the Configuration table to be used. |
| RampUp | Float | The number of seconds the experiment should stay in Ramp Up. Statistics will not be kept for this period. |
| SteadyState | Float | The number of seconds the experiment should stay in Steady State. Statistics will be kept for this period. |
| RampDown | Float | The number of seconds the experiment should stay in Ramp Down. Statistics will not be kept for this period. |
| Tier | Int | The number of tiers to use in a test. |
| PreCmd | Varchar(255) | A command that the Controller should run at the beginning of the test. |
| PreCmdWithRunID | Int | Whether the pre-command should be passed the Token, RunID, DatabaseName, UserName, and the Database NodeName of the test. A 1 indicates that they should be passed; a 0 indicates that they should not be passed. |