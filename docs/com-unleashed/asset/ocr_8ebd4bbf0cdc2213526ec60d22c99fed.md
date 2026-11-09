# # Cloaking

The delegate impersonation level described previously is generally referred to as cloaking. This type of impersonation hides the server’s true identity during calls to other servers by disguising the intermediate server’s identity with the identity of the client.

# # Declarative Security

As you learned in Chapter 8, it is possible to declare the security for a COM server in the registry. This is sometimes called declarative security or per-process security. Note that declarative security and per-process security are not entirely the same. Declarative security consists of the settings in the Windows system registry that are used when a COM server is launched or accessed. Per-process security includes the registry settings but also includes other mechanisms of manipulating the COM server’s settings for the entire process, such as the function `CoInitializeSecurity()`.

In Chapter 13, “Configuring and Error Handling,” you learn how you can use two tools called `DCOMCNFG` and `OLEView` to configure the per-process security settings for your COM servers.

# # Programmatic Security

Earlier in this chapter, you learned two elements of programmatic security—the `IServerSecurity` interface that you used to impersonate the client and the `CoInitializeSecurity()` function used to set per-process security. The `CoInitializeSecurity()` function creates a security blanket for your process; that is, the security settings.

# ## Security Blankets

So what is a security blanket? A security blanket is a set of security properties. Those security properties include the following:

+   - Authentication service
+   - Authorization service
+   - Principal name
+   - Authentication level
+   - Impersonation level
+   - Authentication identity
+   - Capabilities
+   - ACL