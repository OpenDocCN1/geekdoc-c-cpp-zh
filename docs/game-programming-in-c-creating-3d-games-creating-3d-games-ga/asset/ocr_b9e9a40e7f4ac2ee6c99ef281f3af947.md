API, which builds on the Low Level API. However, using the FMOD Studio API does not preclude an audio programmer from accessing the Low Level API if needed. For the most part, this chapter uses the FMOD Studio API.

# Installing FMOD

Because of FMOD’s licensing terms, the book’s source code on GitHub does not include the FMOD library and header files. Luckily, FMOD is free to download and has very favorable licensing terms for commercial projects. (See the FMOD site for details.) To download the FMOD library, go to the FMOD site (https://fmod.com) and create an account.

Once you have an account on the FMOD website, click the Download link. From here, find the downloads for the FMOD Studio API. Make sure you select the version 1.09.09 from the Version dropdown. (Version 1.10.x or newer may not work with this chapter’s code.) Next, select Windows if you’re developing on Windows or Mac if you’re developing on Mac.

On Windows, run the installer and choose the default installation directories. Choosing a different directory doesn’t work out of the box because the Visual Studio project file points directly to the default directories. However, if you really want to install the FMOD API to another directory, you can change the project file (which means changing the include directories, the library directories, and the post-build step that copies DLL files