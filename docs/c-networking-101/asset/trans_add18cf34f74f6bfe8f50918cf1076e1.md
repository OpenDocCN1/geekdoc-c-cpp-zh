
以下是关于如何在 Ubuntu 上安装和配置 Nagios Core 的分步指南。请注意，不同 Linux 发行版的说明可能略有不同：

## 更新系统

首先，更新你的系统软件包：

```bash
sudo apt-get update
```

```bash
sudo apt-get upgrade
```

## 安装所需软件包

接下来，安装所需的软件包：

```bash
sudo apt-get install build-essential libgd-dev openssl libssl-dev unzip apache2 php libapache2-mod-php libperl-dev libltdl-dev wget
```

## 创建 Nagios 用户和组

为 Nagios 创建一个新用户和组：

```bash
sudo useradd nagios
```

```bash
sudo groupadd nagcmd
```

```bash
sudo usermod -a -G nagcmd nagios
```

## 下载并解压 Nagios Core

下载最新版本的 Nagios Core 并解压文件：

```bash
cd /tmp
```

```bash
wget https://github.com/NagiosEnterprises/nagioscore/releases/download/nagios-4.4.6/nagios-4.4.6.tar.gz
```

```bash
tar xzf nagios-4.4.6.tar.gz
```

```bash
cd nagios-4.4.6/
```

## 编译并安装 Nagios

编译并安装 Nagios：

```bash
./configure --with-nagios-group=nagios --with-command-group=nagcmd --with-httpd-conf=/etc/apache2/sites-enabled
```

```bash
make all
```

```bash
sudo make install
```

```bash
sudo make install-init
```

重启 Apache 服务：

```bash
sudo systemctl restart apache2
```

## 下载并安装 Nagios 插件

下载并安装 Nagios 插件：

```bash
cd /tmp
```

```bash
wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz
```

```bash
tar xzf nagios-plugins-2.3.3.tar.gz
```

```bash
cd nagios-plugins-2.3.3/
```

```bash
./configure --with-nagios-user=nagios --with-nagios-group=nagios --with-openssl
```

```bash
make
```

```bash
sudo make install
```

## 启动 Nagios

将 Nagios 服务设置为开机自启动并启动 Nagios：

```bash
sudo systemctl enable nagios
```

```bash
sudo systemctl start nagios
```

之后，你应该可以通过打开 Web 浏览器并导航到 http://your_server_ip/nagios 来访问 Nagios Web 界面。使用用户名 nagiosadmin 和在步骤 7 中创建的密码登录。

请记住将 wget 命令中的 URL 替换为 Nagios 和 Nagios 插件官方网站上提供的最新版本。现在，你可以开始向 Nagios 配置中添加主机和服务以进行监控。

## 在 Nagios 上监控主机和服务

安装 Nagios 后，你可能需要监控网络中的主机（计算机、服务器、路由器等）和服务（HTTP、FTP、SSH 等）。下面介绍如何向 Nagios 配置中添加主机和服务：

### 创建主机和服务定义文件

首先，我们需要为主机和服务创建配置文件。这些文件将放在 /usr/local/nagios/etc/objects 目录中。假设我们要监控一台名为 my-host 的主机。

创建一个新的配置文件：

```bash
sudo nano /usr/local/nagios/etc/objects/my-host.cfg
```

在此文件中，添加以下内容来定义你的主机：

```
define host{

    use             linux-server

    host_name       my-host

    alias           My Host

    address         192.168.1.10

    }
```

请务必将 192.168.1.10 替换为你主机的实际 IP 地址。

### 定义要监控的服务

在同一个 my-host.cfg 文件中，我们可以定义要监控的服务。例如，要监控主机是否在线，以及 SSH 和 HTTP 服务，请添加：

```
define service{

    use             local-service
    host_name              my-host
    service_description   PING
    check_command         check_ping!100.0,20%!500.0,60%
}

define service {
  use                  local-service
  host_name            my-host
  service_description SSH
  check_command        check_ssh
}

define service {
  use                  local-service
  host_name            my-host
  service_description HTTP
  check_command        check_http

}
```

### 将配置文件添加到 Nagios

现在，我们需要让 Nagios 使用我们新的配置文件。打开 Nagios 主配置文件：

```bash
sudo nano /usr/local/nagios/etc/nagios.cfg
```

将以下行添加到文件末尾：

```
cfg_file=/usr/local/nagios/etc/objects/my-host.cfg
```

### 验证并重启 Nagios

在重启 Nagios 之前，我们应该检查配置文件是否有语法错误。使用以下命令：

```bash
sudo /usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

如果没有错误，重启 Nagios：

```bash
sudo systemctl restart nagios
```

现在，Nagios 将开始监控你配置文件中定义的主机和服务。你可以在 Nagios Web 界面上查看状态。

我们使用了 check_ping、check_ssh 和 check_http，这些通常包含在标准 Nagios 插件安装中。

对于其他服务，或者要监控交换机、路由器等网络设备，你可能需要安装额外的插件或使用 SNMP。

## 使用 Nagios 进行故障监控

以下是如何设置 Nagios 进行故障监控的分步指南：

### 安装

首先，你需要在服务器上安装 Nagios。安装过程可能因你使用的操作系统而异。你可以在 Nagios 官方网站上找到详细的安装指南。

### 配置

安装完成后，你需要配置 Nagios 以监控你的网络。主配置文件是 nagios.cfg，位于 Nagios 安装目录中。此文件定义了 Nagios 应在何处查找对象定义文件，这些文件包含主机、服务、联系人等的配置。

### 定义主机和服务

你需要定义希望 Nagios 监控的主机（设备、服务器等）和服务（HTTP、FTP、SMTP 等）。为此，你需要在配置文件中创建对象定义。每个主机和服务定义将包含 Nagios 为确定该主机或服务状态而执行的检查命令。

### 设置警报

Nagios 允许你设置警报，当某个主机或服务宕机或行为异常时，系统会通知你。警报可以通过电子邮件、短信或你已安装的 Nagios 插件支持的任何其他方式发送。

### 开始监控

设置好主机、服务和警报后，你可以启动 Nagios 服务。Nagios 将按照你指定的时间间隔开始检查所定义主机和服务的状态。

### 查看报告

Nagios 提供了一个 Web 界面，你可以在其中查看当前网络状态、通知历史记录、问题历史记录、日志文件和其他有用的报告。

### 维护

定期检查 Nagios 日志，并保持 Nagios 安装和插件为最新版本，以确保平稳运行。

Nagios 可以与 C++ 应用程序一起使用，并且可以通过脚本和各种语言的编译程序（包括 C++）进行扩展和控制，前提是它们遵循 Nagios 插件 API。

### 执行故障监控的示例程序

以下是如何使用 Nagios 执行故障监控的示例。

在之前的步骤中，你已经为主机创建了配置文件并将其添加到 Nagios 配置中。假设你添加了一台名为 my-host、IP 地址为 192.168.1.10 的主机，并且正在监控该主机上的 PING、SSH 和 HTTP 服务。

当 Nagios 开始监控时，它将根据服务定义中指定的 check_interval 定期检查这些服务。如果检测到任何异常，例如服务宕机或响应时间超出可接受范围，它将发出警报。

你可以通过 Nagios Web 界面查看这些警报。为此，请打开 Web 浏览器并访问 http://nagios，然后使用你的 Nagios 帐户登录。

登录后，你会看到 Nagios 仪表板。以下是一些需要注意的关键部分：

