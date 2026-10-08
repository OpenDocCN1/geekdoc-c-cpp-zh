# Using the DRS

The DRS is a simple interface. The following sections outline its use.

# Set Up a Backup Device

Before any backups can happen, you must create a backup device by following these steps:

+   1. In the DRS, navigate to Device > Backup Device.
2. Provide a name for the backup device being created.
3. Specify whether this device is a local tape drive or a network directory (meaning SFTP server).
4. Select the tape drive device or provide the IP address, SFTP root path, and SFTP account the DRS should use.
5. Click Save (up to ten backup devices can be created).

# Create a Scheduled Backup

Now that we have a backup device, we can schedule a backup to use it by following these steps:

+   6. Navigate to Backup > Scheduler.
7. Click Add New.
8. Provide a name for the schedule.
9. Select the previously defined backup device this job should use.
10. Select the features to back up. Depending on the application, these may be:
- CUCM: CCM, CDR CAR
- CUG: CONNECTION_DATABASE, CONNECTION_GREETINGS_VOICE-NAMES, CONNECTION_MESSAGES UNITYBXDBI, CUG
- CUP: CUPS, CUP

+   11. Enable the schedule for the backup.

+   12. Enable the scheduled job.

If desired, a manual backup can be started by navigating to Backup > Manual Backup and performing the same steps, except that instead of defining a schedule, simply start the backup job.

Whether the backup is scheduled or manual, understand that the process is resource-intensive, and it is recommended that they run during times of low demand on the server if possible.

The status of the backup job(s) can be observed by navigating to Backup > Current Status. As one of the components of the backup job and the completion percentage for each component is presented. Components that are complete share a link to the log file.