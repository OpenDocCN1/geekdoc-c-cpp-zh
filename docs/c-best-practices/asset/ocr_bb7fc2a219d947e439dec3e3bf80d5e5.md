# # 46. Use the Tools: Multiple Compilers

Support *at least* 2 compilers on your platform. Each compiler does different analyses and implements the standard in a slightly different way.

If you use Visual Studio, you should be able to switch between clang and cl.exe relatively easily. You can also use WSL and enable remote Linux Builds.

If you use Linux, you should be able to switch between GCC and Clang easily.

On MacOS, be sure the compiler you are using is what you think it is. gcc command is likely a symlink to clang installed by Apple.

For installing newer or different compilers on your platform, the following is available:

Ubuntu / Debian

+   * GCC - Toolchain PPA¹
+   * Clang - apt packages²

Windows

+   * GCC MinGW³
+   * Clang official downloads⁴

¹https://launchpad.net/~ubuntu-toolchain-r/+archive/ubuntu/ppa
²https://apt.llvm.org/
³https://mingw.org/
⁴https://releases.llvm.org/download.html