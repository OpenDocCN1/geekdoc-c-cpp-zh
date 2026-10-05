Restricted tokens are useful when an application wants to impersonate a client at a reduced security level, primarily for safety reasons when running untrusted code. For example, the restricted token can have the shutdown-system privilege removed from it to prevent code executed in the restricted token's security context from rebooting the system.

# Filtered admin token

As you saw earlier, restricted tokens are also used by UAC to create the filtered admin token that all user applications inherit. A filtered admin token has the following characteristics:

+   - The integrity level is set to medium.

+   - The administrator and administrator-SIDs mentioned previously are marked as deny-only to prevent a security hole if the group were to be removed altogether. For example, if a file has an access control list (ACL) that denied the Administrators group all access but granted some to another group the user belongs to, the user would be granted access if the Administrators group was absent from the token, which would give the standard user version of the user's identity more access than the administrator's identity.

+   - All privileges are stripped except Change, Notify, Shutdown, Undock, Increase Working Set, and Time Zone.

# EXPERIMENT: Looking at filtered admin tokens

You can make Explorer launch a process with either the standard user token or the administrator token by following these steps on a machine with UAC enabled:

+   1. Log on to an account that's a member of the Administrators group.

+   2. Open the Start menu, type command, right-click the Command Prompt option that appears, and choose Run as Administrator to run an elevated command prompt.

+   3. Run a new instance of cmd.exe, but this does not it normally (that is, not elevated).

+   4. Run Process Explorer elevated, open the Properties dialog boxes for the two command prompt processes, and click the Security tabs. Note that the standard token contains a deny-only SID and a medium mandatory label, and that it has only a couple of privileges. The properties on the right in the following screenshot are from a command prompt running with an administrator token, and the properties on the left are from one running with the filtered administrator token: