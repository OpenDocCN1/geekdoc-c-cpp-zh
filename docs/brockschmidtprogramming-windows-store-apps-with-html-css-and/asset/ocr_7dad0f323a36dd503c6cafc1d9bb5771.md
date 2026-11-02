Scenario 3 of the sample shows a call to pickSingleFolderAsync defaulting to the desktop, where the result of the operation is a StorageFolder. Here you must indicate a fileTypeFilter that helps users pick an appropriate location where some files of that type exist or create a new location (js/scenario3.js):

```
function pickFolder() {
  // Create the picker object and set options
  var folderPicker = new Windows.Storage.Pickers.FolderPicker();
  folderPicker.suggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.desktop;
  folderPicker.fileTypeFilter.replaceAll([".docx", ".xlsx", ".pptx"]);
  folderPicker.pickSingleFolderAsync().then(function (folder) {
    if (folder) {
      // Cache folder so the contents can be accessed at a later time
      Windows.Storage.AccessCache.StorageApplicationPermissions.FutureAccessList
        .addOrReplace("PickedFolderToken", folder);
    } else {
      // The picker was dismissed with no selected file
    }
  });
}
```

You can see here that we save the folder in the access cache, which we'll come back to shortly. First let's look at the final file picker use case in scenario 4, where we use a FileSavePicker object and its pickSaveFileAsync method (js/scenario4.js), resulting in the UI of Figure 11-10 (assuming SkyDrive is the default save location; I've also added the myData variable to illustrate what's being saved, even though it isn't in the sample):

```
function saveFile(myData) {
  // Create the picker object and set options
  var savePicker = new Windows.Storage.Pickers.FileSavePicker();
  savePicker.suggestedStartLocation = Windows.Storage.Pickers.PickerLocationId.documentsLibrary;
  // Drop-down of file types the user can save the file as
  savePicker.fileTypeChoices.insert("Plain Text", [".txt"]);
  // Default file name if the user does not type one in or select a file to replace
  savePicker.suggestedFileName = "New Document";
  savePicker.pickSaveFileAsync().done(function (file) {
    if (file) {
      // Prevent updates to the remote version of the file until we finish making changes and call CompleteUpdatesAsync.
      Windows.Storage.CachedFileManager.deferUpdates(file);
      // write to file
      Windows.Storage.FileIO.writeTextAsync(file, myData).done(function () {
        // Let Windows know that we're finished changing the file so the other app can update the remote version of the file (see Appendix D).
        // Completing updates might require Windows to ask for user input.
        Windows.Storage.CachedFileManager.completeUpdatesAsync(file)
          .done(function (updateStatus) {
            if (updateStatus ===
              Windows.Storage.Provider.FileUpdateStatus.complete) {
```