We start by installing GLEW and GLFW. Probably the easiest way to install these libraries is by using the “Homebrew” tool. Homebrew is a package manager designed to make the installation of commonly needed utilities on the Mac as easy as possible. The steps for installing Homebrew are as follows:

+   1. Open the Safari browser, and visit the Homebrew website (**https://brew.sh**).
+   2. Follow the installation instructions on the homebrew page. Specifically, copy the line of code given in the center of the page, open a terminal window on the Mac, paste the copied command into it, and hit return. You may need to enter your Mac password.
+   3. Leave the terminal window open; we will use it again in the next steps.

Next, use the newly installed Homebrew utility to install GLEW and GLFW, as follows:

+   1. Still at the terminal prompt, enter the command: brew install glfw3
+   2. Still at the terminal prompt, enter the command: brew install glew
+   3. Note that two folders have been added to **/usr/local/include**, named **GL** and **GLFW**.

Next we install the math library GLM. Of the four libraries, this is the simplest. Since GLM is a header-only library, simply: (a) download and uncompress the library as described earlier in Section A.1.5, then (b) copy the resulting “glm” folder and its contents to **/usr/local/include**.

Installing SOIL2 is probably the trickiest of the four libraries to install. The steps we have used successfully are as follows:

+   1. Download the Mac versions of **SOIL2** and **premake** (version 5).
+   2. Uncompress **premake**. The only file in it is a premake executable.
+   3. Copy the **premake** executable into the SOIL2 folder.
+   4. In a terminal window, navigate to the SOIL2 folder and enter:
+      ```
+      ./premake5 gmake
+      ```
+   5. Still in the SOIL2 folder, enter cd make/macosx to navigate into the make folder, then type:
+      ```
+      make
+      ```
+   6. **SOIL2** should build successfully—the test files might not (it’s ok, they aren’t important to us). The build should produce a “**src/SOIL2**” folder that includes several .h files, and a “**lib**” folder that includes a library file named “**libsoil2-debug.a**”.