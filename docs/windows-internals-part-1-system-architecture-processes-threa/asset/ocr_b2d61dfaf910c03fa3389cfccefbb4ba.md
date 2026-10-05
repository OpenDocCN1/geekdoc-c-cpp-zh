# EXPERIMENT: The Bypass Traverse Checking privilege

If you are a systems administrator, you must be aware of the Bypass Traverse Checking privilege (internally called SeNotifyPrivPrivilege) and its implications. This experiment demonstrates that not understanding its behavior can lead to improperly secured service.

+   1. Create a folder and, within that folder, a new text file with some sample text.

+   2. Navigate in Explorer to the new file, open its Properties dialog box, and click the **Security** tab.

+   3. Click the **Advanced** button.

+   4. Deselect the **Inheritance** check box.

+   5. Select **Copy** when you are prompted as to whether you want to remove or copy inherited permissions.

+   6. Modify the security of the new folder so that your account does not have any access to the folder. To do so, select and check all the **Deny** boxes in the permissions list.

+   7. Run Notepad. Then open the **File** menu, choose **Open**, and browse to the new directory in the dialog box that appears. You should be denied access to the directory.

+   8. In the File Name field of the Open dialog box, type the full path of the new file. The file should open.

If your account does not have the Bypass Traverse Checking privilege, NTFS prevents an access check on each directory of the path to a file when you try to open a file, which results in being denied access to the file in this example.

# Super privileges

Several privileges are so powerful that a user to which they are assigned effectively a "super user" who has full control over a computer. These privileges can be used in an infinite number of ways to gain unauthorized access to off-limit resources and to perform unauthorized operations. However, we will focus on using the privilege to execute code that the user privileges not assigned to the user, with the knowledge that this capability can be leveraged to perform any operation on the local machine that the user desires.

This section lists the privileges and discusses some of the ways they can be exploited. Other privileges, such as Lock Pages in Physical Memory (SeLockMemoryPrivilege), can be exploited for denial-of-service attacks on a system, but these are not discussed. Note that systems with UAC enabled, these privileges will be granted only to applications running at high integrity level or higher, even if the account possesses them: