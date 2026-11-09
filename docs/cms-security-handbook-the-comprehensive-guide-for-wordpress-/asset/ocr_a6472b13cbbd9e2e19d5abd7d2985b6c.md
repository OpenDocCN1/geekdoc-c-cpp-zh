Finally, you want some form of logging. Logging systems or software should include the date and time of the backup, who conducted it, what issues (if any) were encountered, what was backed up, and where the backup is located. Many other data points could be captured in this log that enable you to make that determination. As you draft your policy, be sure you don’t forget things such as e-mail that may be on your server as well. Don’t forget to review your discovery questions to ensure that you didn’t miss anything.

In essence, your backup policy is to guide you and your staff in the handling and disposition of the data. It should be clear, concise, and easy to follow.

In regard to specific hardware solutions, it all depends on your need and your budget.

For a small business, a local Linear Tape Open (LTO) tape taken nightly or weekly and stored offsite might be sufficient. For example, you might want to review the BackupExec software for small business: (www.symantec.com/business/products/family.jsp?prid=backupexec). This would provide you with the logging needed and the capability to recover.

When you grow into a medium-sized business, you want to “break the tape habit” by moving into an offsite replication or data-duplication solution. You might consider using a product such as the Dell EqualLogic storage system (www.equallogic.com) to create a local snapshot, and then replicate that to an offsite EqualLogic box. The replicated storage machine would then do a snapshot in the remote machine. This gives you multiple backups and a means of recovery.

Additionally, in a medium-sized environment, you will likely be deploying some form of virtual computing (such as VMware) in that environment. Using a mix of the EqualLogic and the Quantum solution for virtual backups (www.quantum.com/Solutions/Virtualization/Index.aspx) would enable the logging and protection you need.

> > **NOTE**  For more detailed information on the entirety of planning and implementing backups, see the book, *Implementing Backup and Recovery: The Readiness Guide for the Enterprise* by David Little and David Chapa (Indianapolis: Wiley, 2003).

# Server-Side Backup and Restoration Methods

The cPanel utility includes a great facility for backing up your web server. Incorporating this method into your plans is easy to do, and provides a full backup of your website. The downside to this tool is that it does a full backup, and the file can quickly grow in size. If that’s what you need, however, then there should be no problem. The size of the files could be large and take a little time to deal with during a download.