![](bbox=[0.215, 0.128, 0.893, 0.543])

**Figure 10.12** Launching a signed applet

For intranet deployment, certificates are more plausible. Administrators can install policy files and certificates on local machines so that no user interaction is required for launching trusted code. Whenever the Java plug-in tool loads signed code, it consults the policy file for the permissions and the keystore for signatures.

For the remainder of this section, we will describe how you can build policy files that grant specific permissions to trusted code.

Suppose ACME Software wants its employees to run certain programs that require local file access, and it wants to deploy these programs through a browser as Web Start applications.

As you saw earlier in this chapter, ACME could identify the programs by their code base. But that means ACME would need to update the policy files each time the programs are moved to a different web server. Instead, ACME decides to *sign* the JAR files that contain the program code.