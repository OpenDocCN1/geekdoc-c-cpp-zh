Below is a step-by-step walkthrough on how to install and configure Nagios Core on Ubuntu. Please note that instructions may vary slightly for different Linux distributions:

# Update System

First, update your system packages:

```
sudo apt-get update
```

```
sudo apt-get upgrade
```

# Install Required Packages

Next, install the required packages:

```
sudo apt-get install build-essential libgd-dev openssl libssl-dev unzip apache2 php libapache2-mod-php libperl-dev libltdl-dev wget
```

# Create Nagios User and Group

Create a new user and group for Nagios:

```
sudo useradd nagios
```

```
sudo groupadd nagcmd
```