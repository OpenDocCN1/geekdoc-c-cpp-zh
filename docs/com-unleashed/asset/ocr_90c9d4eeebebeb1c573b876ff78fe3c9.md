![](bbox=[0.148, 0.114, 0.663, 0.259])

The next few sections describe the various settings in the OLE registry subkey.

# Enabling and Disabling DCOM

The EnableDCOM value enables you to enable and disable remote objects. Setting this value to N disables remote objects but does not disable DCOM security.

# Default Permissions

The DefaultLaunchPermission and DefaultAccessPermission values are used when a COM server does not provide values in its AppID key for the LaunchPermission and AccessPermission. If the AppID’s AccessPermission is missing, the DefaultLaunchPermission is used. If the AppID’s AccessPermission is missing, the DefaultAccessPermission is used.

Managing the permissions for hundreds of COM servers on your machine on an individual basis is not really possible. Therefore, I have taken the approach to use the default permissions rather than configure COM servers individually. If a COM server proves that it needs additional or less security, then and only then do I add custom permissions.

# Legacy Security

COM+ provides values to set default security settings that apply to components that do not implement specific security in these areas. The following authentication levels are available:

+   - `RPC_C_AUTHN_LEVEL_DEFAULT`—Uses the authentication service’s default authentication level.
+   - `RPC_C_AUTHN_LEVEL_NONE`—No authentication.
+   - `RPC_C_AUTHN_LEVEL_CONNECT`—Authenticates only at connection.
+   - `RPC_C_AUTHN_LEVEL_CALL`—Authenticates every call.
+   - `RPC_C_AUTHN_LEVEL_PKT`—Authenticates every packet.