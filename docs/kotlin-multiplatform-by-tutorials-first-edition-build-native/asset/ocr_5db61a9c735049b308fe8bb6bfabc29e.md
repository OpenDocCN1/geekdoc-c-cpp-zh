# ## AddTimeZoneDialog

Open AddTimeZoneDialog.kt from the
commonMain/kotlin/com/raywenderlich/compose/ui folder inside the
shared-ui module. You’ll see several errors for the following imports:

> import androidx.compose.ui.res.stringResource
> import androidx.compose.ui.window.Dialog
> import com.raywenderlich.findtime.android.R

These three imports don’t exist for the shared-ui module. Remove them. After
the imports add:

> @Composable
> expect fun AddTimeDialogWrapper(onDismiss: onDismissType, content: @Composable () -> Unit)

This is a Composable function that uses KMM’s expect keyword. This means
that each target this module uses needs to implement this function. Now,
change the signature for the AddTimeZoneDialog function and the code up to
the first Column with the following code:

> fun AddTimeZoneDialog(
> onAdd: OnAddType,
> onDismiss: onDismissType
> ) {
>     val timezoneHelper: TimeZoneHelper = TimeZoneHelperImpl()
> 
>     AddTimeDialogWrapper(onDismiss) {
> }

This just uses the AddTimeDialogWrapper function to wrap the existing code.
The AddTimeDialogWrapper function will handle platform-specific code.
Android will handle the dialog one way, and the desktop another way. Go to the
end of this function and add an ending }.

One issue in using Desktop Compose is resource handling. That’s beyond the
scope of this chapter. For now, just change the string resources to hard-coded
strings. Change:

> stringResource(id = R.string.cancel)