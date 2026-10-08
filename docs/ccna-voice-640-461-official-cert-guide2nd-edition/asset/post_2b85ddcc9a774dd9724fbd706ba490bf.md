
# Describe the Disaster Recovery System

The Disaster Recovery System (DRS) allows administrators to perform scheduled backups or manual backups of the CUCM and CDR/CAR databases. It also backs up and restores its own configuration settings, so in the event of a restore, the DRS does not have to be totally reconfigured.

The DRS includes GUI and CLI user interfaces, a backup scheduler, tape or SFTP backup storage, and a distributed system architecture for backup and restore functions. Backups must be restored to the same version of the application. The DRS cannot be used as an upgrade/downgrade mechanism, although it can be used to migrate from a physical server to a VMware server.

The DRS architecture features a Local Agent on each server in the cluster (which performs the backup and restore operations), and a Master Agent on the Publisher. The Master Agent does the following:

- Stores system-component registration information.
- Maintains the schedule of backup tasks and sends the tasks to the Local Agents as scheduled.
- Stores backups on a local tape drive or a remote SFTP server.
- Interfaces with the administrator via the DRS web page.

The DRS web interface is accessed at https://<ip address>/drf or by using the drop-down navigation selection at the top-right of the CUCM administration page. By default, only the Platform Administration account has access to the DRS, but other accounts can be given the necessary privilege.

The DRS is a common feature of all Linux-based Unified Communications applications, but different components are backed up based on the application. Table 16-2 lists the components that can be backed up for CUCM, CUC, and CUP.

## Table 16-2 Components Backed Up by DRS

| CUCM | CUP | CUC |
|---|---|---|
| Platform | Platform | Platform |
| Cisco License Manager | Cisco License Manager | Cisco License Manager |
| Trace Collection Tool | Trace Collection Tool | Trace Collection Tool |
| Syslog | Syslog | Syslog |
| CUCM DB | CUP DB | CUC DB |
| TFTP/MoH Files | XCP Data | Mailbox Store |
| CDR/CAR Data | CUP Data | Greetings |

# Using the DRS

The DRS is a simple interface. The following sections outline its use.

## Set Up a Backup Device

Before any backups can happen, you must create a backup device by following these steps:

1. In the DRS, navigate to Device > Backup Device.
2. Provide a name for the backup device being created.
3. Specify whether this device is a local tape drive or a network directory (meaning SFTP server).
4. Select the tape drive device or provide the IP address, SFTP root path, and SFTP account the DRS should use.
5. Click Save (up to ten backup devices can be created).

## Create a Scheduled Backup

Now that we have a backup device, we can schedule a backup to use it by following these steps:

6. Navigate to Backup > Scheduler.
7. Click Add New.
8. Provide a name for the schedule.
9. Select the previously defined backup device this job should use.
10. Select the features to back up. Depending on the application, these may be:
    - CUCM: CCM, CDR CAR
    - CUG: CONNECTION_DATABASE, CONNECTION_GREETINGS_VOICE-NAMES, CONNECTION_MESSAGES UNITYDBI, CUG
    - CUP: CUPS, CUP

11. Enable the schedule for the backup.

12. Enable the scheduled job.

If desired, a manual backup can be started by navigating to Backup > Manual Backup and performing the same steps, except that instead of defining a schedule, simply start the backup job.

Whether the backup is scheduled or manual, understand that the process is resource-intensive, and it is recommended that they run during times of low demand on the server if possible.

The status of the backup job(s) can be observed by navigating to Backup > Current Status. As one of the components of the backup job and the completion percentage for each component is presented. Components that are complete share a link to the log file.

# Perform a Restore

The purpose of having backups is to be able to restore the data when necessary: The following steps describe the basic restore process:

1. Navigate to Restore > Restore Wizard.
2. Select the device that holds the backup file from which you wish to restore.
3. Select the correct backup file from the list available on that device.
4. Select the feature(s) you want to restore. It should be self-evident that if a feature was not backed up, it cannot be restored!
5. If the restore is coming from an SFTP server, you may select the optional File Integrity Check, which ensures that the restored data is not corrupted. Doing so takes significant server and network resources and slows down the restore process.
6. Select the server(s) that should be restored. If the Publisher (first node) is selected for restore, the DRS automatically restores the database on the subscribers (subsequent nodes). However, in either case, all existing data is overwritten by the restore.
7. Monitor the restore progress by navigating to Restore > Status.

Administrators should be familiar with the content of the Disaster Recovery System Administration Guide for their version(s) of software and should practice restore scenarios in a lab environment.

# Exam Preparation Tasks

## Review All the Key Topics

Review the most important topics in the chapter, noted with the key topics icon in the outer margin of the page. Table 16-3 describes these key topics and identifies the page number on which each is found.

| Key Topic Element | Description | Page Number |
| --- | --- | --- |
| List | troubleshooting | 419 |
| Topic | IP Phone | 419 |
| Topic | Generating CDR | 427 |
| Topic | Generating system | 430 |
| Topic | Cisco RTMT | 432 |
| Topic | Describe Disaster Recovery | 434 |

## Definitions of Key Terms

Define the following terms from this chapter, and check your answers in the Glossary: troubleshooting, Call Detail Record (CDR), Call Management Record (CMR), Disaster Recovery System (DRS)

This chapter includes the following topics:

- Generating and Accessing Unity Connection Reports: This section reviews how to create and locate.
- Analyzing Unity Connection Reports: This section examines the content of.
- Troubleshooting and Maintenance Operations Using Unity Connection Reports: This section provides guidance and examples for using.

![](img/e47862dc47b4e5de0cde3b4550ad65)

# Monitoring Cisco Unity Connection

Cisco Unity Connection (CUC) includes a variety of built-in reports to help administrators track the server's health and performance, as well as the activities of the users. This chapter introduces the use of many of these reports.

## “Do I Know This?” Quiz

The “Do I Know This?” quiz allows you to assess whether you should read this entire chapter or simply jump to the “Exam Preparation” section for review. If you are in doubt

| Foundation Topics Section | Question |
| --- | --- |
| Generating and Accessing Unity Connection Reports | 1–6 |
| Analyzing Unity Connection Reports | 7–8 |
| Troubleshooting and Maintenance Operations Using Unity Connection Reports | 9–10 |

- Cisco Unity Connection provides two built-in reporting interfaces. Name them. (Choose two).
- a Cisco Unified Reporting
- b Cisco Unity Connection Reporting
- c Cisco Unity Connection Serviceability Tool
- d Cisco Unified Serviceability Archive

2. Which of the following is not a Unity Connection Serviceability Tool report?

- a Server Report
- b Unused Voice Accounts Report
- c User Lockout Report
- d Port Activity Report
- e Users Report

3. Which of the following are Unified Serviceability Archive reports? (Choose two).

- a Mailbox Store Report
- b Alert Report
- c System Configuration Report
- d Server Report
- e Message Traffic Report

4. What service must be activated in order to begin the collection of the Unified Serviceability Archive report data?

- a Cisco Serviceability Reporter
- b Cisco UXL Web Service
- c Cisco Reports Harvester
- d Cisco Unity Connection Serviceability Harvester

5. How many reports are available in the Unified Serviceability Archive?

- a 19
- b 2
- c 19 per day
- d 2 per day of data collection

6. You decide to increase the number of entries that can be held in the Audit Log. Where can this be done?

- a It cannot be done.
- b It is done by saving old log files to a syslog server and removing them from the original log location.
- c It is done in the Service Parameters configuration page.
- d In CUC Administration, navigate to System Settings > Advanced > Reports.
