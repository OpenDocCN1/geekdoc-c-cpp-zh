The `SERVICE_STATUS::dwControlsAccepted` member can have the following values:

+   - `SERVICE_ACCEPT_STOP`—The service can be stopped.
+   - `SERVICE_ACCEPT_PAUSE_CONTINUE`—The service can be paused and unpaused.
+   - `SERVICE_ACCEPT_SHUTDOWN`—The service can be shut down.
+   - `SERVICE_USER_DEFINED_CONTROL`—The service accepts user-defined control messages.

`SERVICE_STATUS::dwWin32ExitCode` and `SERVICE_STATUS::dwServiceSpecificCode` members can be used to report errors to the SCM. A service can pass a Win32 error code by setting the `SERVICE_STATUS::dwWin32ExitCode` member. Or, a service can pass a proprietary error code by setting `SERVICE_STATUS::dwWin32ExitCode` to `ERROR_SERVICE_SPECIFIC_ERROR` and setting `SERVICE_STATUS::dwServiceSpecificCode` to the error code.

The `SERVICE_STATUS::dwCheckPoint` and `SERVICE_STATUS::dwWaitHint` members indicate to the SCM the progression of the services initialization or shutdown. `SERVICE_STATUS::dwCheckPoint` should be incremented with each call to the `SetServiceStatus()` function to indicate progress in the initialization or shutdown. The `SERVICE_STATUS::dwWaitHint` member should indicate the maximum amount of time in milliseconds that should elapse between the current call to the `SetServiceStatus()` function and the next call to the same function. If the time elapses before the next call to the `SetServiceStatus()` function, the SCM assumes that your service is not operating properly and suspends it.

When your service is properly initialized and registered by calling the `RegisterServiceCtrlHandler()` function, the SCM begins sending messages to your `ServiceCtrlHandler()` callback function.

# ServiceCtrlHandler()

The `ServiceCtrlHandler()` function can receive five standard messages. You can also add additional control messages in the range 128–256. The five standard messages are as follows:

+   - `SERVICE_CONTROL_PAUSE`—The SCM is requesting that the service pause itself.
+   - `SERVICE_CONTROL_CONTINUE`—The SCM is requesting that the service unpause itself.
+   - `SERVICE_CONTROL_STOP`—The SCM is requesting that the service shut itself down.
+   - `SERVICE_CONTROL_SHUTDOWN`—The system is being shut down.
+   - `SERVICE_CONTROL_INTERROGATE`—The SCM is requesting the status of the service.