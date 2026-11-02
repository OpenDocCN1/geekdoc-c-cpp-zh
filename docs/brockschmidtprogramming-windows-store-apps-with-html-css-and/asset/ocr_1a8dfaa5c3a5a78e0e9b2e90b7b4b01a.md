list instead.)

+   6. `Windows.UI.WebUI.WebUIApplication.onactivated` fires. This is typically where you'll do all your startup work, instantiate WinJS and custom controls, initialize state, and so on.

Once the `activated` event handler returns, the default splash screen is dismissed unless the app has requested a deferral, as discussed later in the “Activation Deferrals and setPromise” section.With the latter four events, your app’s handling of these very much determines how quickly it comes up and becomes interactive. It almost goes without saying that you should strive to optimize that process, a subject we’ll return to a little later in “Optimizing Startup Time.”

What’s also different between an app and a website is that an app can again be activated for many different purposes, such as contracts and associations, even while it’s already running. As we’ll see in later chapters, the specific page that gets loaded (step 3) can vary by contract, and if a particular page is already running it will receive only the `Windows.UI.WebUI.WebUIApplication.onactivated` event and not the others.

For the time being, though, let’s concentrate on how we work with this core launch process, and because you’ll generally do your initialization work within the `activated` event, let’s examine that structure more closely.

# Sidebar: File Encoding for Best Startup Performance

To optimize bytecode generation when parsing HTML, CSS, and JavaScript, which speeds app launch time, the Windows Store requires that all .html, css, and .js files are saved with Unicode UTF-8 encoding. This is the default for all files created in Visual Studio or Blend. If you’re importing assets from other sources including third-party libraries, check this encoding: in Visual Studio’s File Save As dialog (Blend doesn’t have a Save As feature), select Save with Encoding and set that to Unicode (UTF-8 with signature) – Codepage 65001. The Windows App Certification Kit will issue warnings if it encounters files without this encoding.

![](bbox=[0.13, 0.75, 0.78, 0.9])

Along these same lines, minification of JavaScript isn’t particularly important for Windows Store apps. Because an app package is downloaded from the Windows Store as a unit and often contains other assets that are much larger than your code files, minification won’t make much difference there. Once the package is installed, bytecode generation means that the package’s JavaScript has already been processed and optimized, so minification won’t have any additional performance impact. If your intent is to obfuscate your code (because it is just there in source form in the installation folder), see “Protecting Your Code” in Chapter 18, “WinRT Components.”