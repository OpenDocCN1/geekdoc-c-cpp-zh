
## Testing Your Plan

Now that you have written your plan, and believe you have captured everything you need, take a deep breath. Your plan is about to break. It's guaranteed that it will not withstand the first few run-throughs. Don't let this concern you or even dissuade you. It's simply how things work.

Testing the plan in advance of really needing to implement it is obviously better. In the context of your personnel, make sure you let them follow the written plan during the test, and encourage them to make notes on where it failed.

This section lays out three steps of the test cycle:

- 1. Do what is basically a desktop or paper exercise.
- 2. Test various portions of your plan to make sure they work individually.
- 3. Conduct a real test where you either simulate a failure, or you run the test live on a backup system.

### Performing a Desktop Test

The desktop test is in essence a paper exercise. What you should do is conduct this test as if you were really doing the drill. However, this will just be verbalizing the actions. Talk each step through. Ask a lot of questions, such as “Is this right?” or “Is there an alternative approach?”

The intent is to ensure that the approach works, the roles are understood by everyone, and minor (or major) steps are not missed.

### Using a Phased Approach

In the second step of your testing, you use a phased approach to do the hands-on testing of various components of your system. For example, one phase might be obtaining a backup tape or CD/DVD from an offsite locker, and restoring it to a test server. Another part of the plan may actually be bringing up your spare e-mail server, or activating a new web server in place of the old.

The phases should also include any non-technical tasks, such as contacting everyone on a call list. This call list should be tested as part of either the phased approach or dry runs. Like any other business process, this should be monitored for updates and changes. Establishing a central repository for the results may be the function of the HR department. The HR representative could provide regular updates of key players.

During this phased approach, any findings that differ from the expected results should be documented and the action retested.

### Conducting a Live Test

The final step is an end-to-end test of your plan. If you have a very complex system, you may choose to test individual portions of your services separately.

In this step, you may schedule an outage to test the real capacities of your plan. Or, as an alternative, set up an identical environment on one of the public cloud services. The results you are looking for ensure that you have met your recovery objectives in your plan and that you have minimized downtime as much as possible.

Perform your drills for this step until you are satisfied with the responses. Then look at a regular (6 months or so) test of the plan.

Again, a safe bet is that you’ll have some issues and hiccups. Don’t sweat it. Learn from it, modify your plan, and move on.

If you have any major changes to your infrastructure, you will need to revisit and adjust the plan. And, of course, retest.

### Performing a Post-Test Review

At the end of the event, all team members should gather and review the event. This report (the *After Action Report*) is designed to capture information while it is fresh — what went right, what went wrong, what the root cause of the failure was, and so on.

Consider all the information in the After Action Report. You should reformulate your plan if there are (and there will be) errors and issues with the plan. This should not be a punitive event. If it’s seen as such, you’re guaranteed to have less cooperation next time.

Following are some sample questions for the post-disaster meeting:

- Why did the event happen? Be sure to look at mundane things such as patching or updates that were missed.
- What risk was not mitigated or eliminated (if any)?
- Where did the plan have holes that need to be closed?
- What can the leader(s) do better next time?
- What can the staff do better next time?
- What went right?
- What feedback from the user community did you receive?
- Have you addressed all stakeholders’ concerns (including customers, both internal and external) in a timely fashion?
- Is there any bad press that must be dealt with?

Incorporate these things into your plan, and schedule a disaster drill soon after to ensure that the plan has successfully been updated.

The post-test review is where you formulate your After Action Report. Chances are good that if you have convinced the senior management team to spend the money on developing a disaster recovery plan, they’re going to want to know the results. If the test doesn’t go well, the impression might be that it was a waste of money and time. It’s only a waste, however, if no improvements are made as a result of the tests.

As part of your test, you should have a trusted and neutral person monitor and observe. That person’s role will be to gauge reactions, check on progress, and, basically, just see how the test goes.

After the test is done, schedule a follow-up for just the leadership within a few days. Ask the person monitoring for a candid review of the leadership’s performance. You may hear some things you don’t want to hear, but your finding them out now is better than finding them out in a real emergency. Gather feedback on the staff’s performance — good, bad, and ugly. You can use this information to improve performance on all fronts.

Technical glitches that are found should be brought up in a staff meeting dedicated to gathering impressions, facts, ideas, and changes. If you trust your staff, then trust their impressions. Update your materials and redistribute the changes to the plan.

What you may find is that some procedures that were documented don’t actually work. For example, in a real-life situation the documentation from a hardware manufacturer was inaccurate for a large uninterruptible power supply (UPS). This huge piece of equipment had a particular stop and startup procedure. The documentation was wrong, and the test discovered it. Had this discovery been made during an active disaster, the company’s time to recover would have been much longer.

You should consider retesting your plan within 90 to 120 days.

## Anticipating the Unexpected

You should always expect to find the unexpected, whether that be during a test or during any real disaster. Do not expect your well-oiled plans to work every time. Expect failures. Expect resistance from the websites and technologies. Because disasters are typically chaotic moments, expect some of that chaos to rub off on your process. The phenomenon touches people, processes, technology, missed shipments, and more. These are simply part of the event.

## Identifying a Basic Backup Policy

Your backup policy is a guide that you will write that dictates the how, when, and the frequency with which you back up your sites and systems.

Finally, you want some form of logging. Logging systems or software should include the date and time of the backup, who conducted it, what issues (if any) were encountered, what was backed up, and where the backup is located. Many other data points could be captured in this log that enable you to make that determination. As you draft your policy, be sure you don’t forget things such as e-mail that may be on your server as well. Don’t forget to review your discovery questions to ensure that you didn’t miss anything.

In essence, your backup policy is to guide you and your staff in the handling and disposition of the data. It should be clear, concise, and easy to follow.

In regard to specific hardware solutions, it all depends on your need and your budget.

For a small business, a local Linear Tape Open (LTO) tape taken nightly or weekly and stored offsite might be sufficient. For example, you might want to review the Backup Exec software for small business: (www.symantec.com/business/products/family.jsp?prid=backupexec). This would provide you with the logging needed and the capability to recover.

When you grow into a medium-sized business, you want to “break the tape habit” by moving into an offsite replication or data-duplication solution. You might consider using a product such as the Dell EqualLogic storage system (www.equallogic.com) to create a local snapshot, and then replicate that to an offsite EqualLogic box. The replicated storage machine would then do a snapshot in the remote machine. This gives you multiple backups and a means of recovery.

Additionally, in a medium-sized environment, you will likely be deploying some form of virtual computing (such as VMware) in that environment. Using a mix of the EqualLogic and the Quantum solution for virtual backups (www.quantum.com/Solutions/Virtualization/Index.aspx) would enable the logging and protection you need.

> **NOTE** For more detailed information on the entirety of planning and implementing backups, see the book, *Implementing Backup and Recovery: The Readiness Guide for the Enterprise* by David Little and David Chapa (Indianapolis: Wiley, 2003).

### Server-Side Backup and Restoration Methods

The cPanel utility includes a great facility for backing up your web server. Incorporating this method into your plans is easy to do, and provides a full backup of your website. The downside to this tool is that it does a full backup, and the file can quickly grow in size. If that’s what you need, however, then there should be no problem. The size of the files could be large and take a little time to deal with during a download.
