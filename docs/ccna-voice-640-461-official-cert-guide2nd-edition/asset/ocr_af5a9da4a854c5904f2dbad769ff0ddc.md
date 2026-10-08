# Describe the Disaster Recovery System

The Disaster Recovery System (DRS) allows administrators to perform scheduled backups or manual backups of the CUCM and CDR/CAR databases. It also backs up and restores its own configuration settings, so in the event of a restore, the DRS does not have to be totally reconfigured.

The DRS includes GUI and CLI user interfaces, a backup scheduler, tape or SFTP backup storage, and a distributed system architecture for backup and restore functions. Backups must be restored to the same version of the application. The DRS cannot be used as an upgrade/downgrade mechanism, although it can be used to migrate from a physical server to a VMware server.

The DRS architecture features a Local Agent on each server in the cluster (which performs the backup and restore operations), and a Master Agent on the Publisher. The Master Agent does the following:

+   - Stores system-component registration information.
- Maintains the schedule of backup tasks and sends the tasks to the Local Agents as scheduled.
- Stores backups on a local tape drive or a remote SFTP server.
- Interfaces with the administrator via the DRS web page.

The DRS web interface is accessed at https://<ip address>/drf or by using the drop-down navigation selection at the top-right of the CUCM administration page. By default, only the Platform Administration account has access to the DRS, but other accounts can be given the necessary privilege.

The DRS is a common feature of all Linux-based Unified Communications applications, but different components are backed up based on the application. Table 16-2 lists the components that can be backed up for CUCM, CUC, and CUP.

Table 16-2 Components Backed Up by DRS

| CUCM | CUP | CUC |
|---|---|---|
| Platform | Platform | Platform |
| Cisco License Manager | Cisco License Manager | Cisco License Manager |
| Trace Collection Tool | Trace Collection Tool | Trace Collection Tool |
| Syslog | Syslog | Syslog |
| CUCM DB | CUP DB | CUC DB |
| TFTP/MoH Files | XCP Data | Mailbox Store |
| CDR/CAR Data | CUP Data | Greetings |