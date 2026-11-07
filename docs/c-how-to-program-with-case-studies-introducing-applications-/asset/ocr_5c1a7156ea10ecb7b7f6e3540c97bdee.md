+   6. Confirm that gcc is installed by executing the following command:

```
```
gcc --version
```
```

To access our code files, use the cd command to change the folder within Ubuntu to:

```
```
cd /mnt/c/Users/YourUserName/Documents/examples
```
```

Use your own user name and update the path to where you placed our examples on your system.

# ### GNU Compiler Collection (GCC) Docker Container

Docker is a tool for packaging software into containers (also called images) that bundle everything required to execute software across platforms. Docker is particularly useful for software packages with complicated setups and configurations. You typically can download preexisting Docker containers (often at https://hub.docker.com) for free and execute them locally on your desktop or notebook computer. This makes Docker a great way to get started with new technologies quickly and conveniently.

Docker makes it easy to use the GNU Compiler Collection on most versions of Windows 10, and on macOS and Linux. The GNU Docker containers are located at

https://hub.docker.com/_/gcc

# ### Installing Docker

To use the GCC Docker container, first install Docker. Windows (64-bit)^3 and macOS users should download and run the Docker Desktop installer from:

https://www.docker.com/get-started

then follow the on-screen instructions. Linux users should install Docker Engine from:

https://docs.docker.com/engine/install/

Also, sign up for a Docker Hub account on this webpage so you can install pre-configured containers from https://hub.docker.com.

# ### Downloading the Docker Container

Once Docker is installed and running, open a Command Prompt (Windows), Terminal (macOS/Linux) or shell (Linux), then execute the command:

```
```
docker pull gcc:latest
```
```

Docker downloads the GNU Compiler Collection (GCC) container's current version.^4 In one of Section 1.10's test-drives, we'll demonstrate how to execute the container and use it to compile and run C programs.

+   3. If you have Windows Home (64-bit), follow the instructions at https://docs.docker.com/docker-for-windows/install-windows-home/.
+   4. At the time of this writing, the current version of the GNU Compiler Collection is 10.2.