# Windows Subsystem for Linux

This documentation is designed to offer a detailed, step-by-step guide for configuring the Windows Subsystem for Linux (WSL) on your target machine.

# Purpose

The purpose of this document is to provide guidance for setting up a new WSL instance, installing all the necessary tools, and the maintanance of them.

# Overview

The Windows Subsystem for Linux (WSL) enables us to run a GNU/Linux environment, complete with a wide range of command-line tools, utilities, and applications, directly on Windows. This can be accomplished without making any modifications to the Linux environment, and it avoids the resource overhead associated with traditional virtual machines or dual-boot configurations.

# Table of Contents

1. [Prerequisites](#prerequisites)
2. [WSL installation](#wsl-installation)
3. [Install WSL command](#install-wsl-command)
4. [WSL shell](#wsl-shell)
5. [Change the default Linux distribution installed](#change-the-default-linux-distribution-installed)
6. [Set up Linux username and password](#set-up-linux-username-and-password)
7. [Update WSL](#update-wsl)
8. [Supported WSL versions](#supported-wsl-versions)
9. [Configuring DNS](#configuring-dns)
10. [Update and upgrade packages](#update-and-upgrade-packages)
11. [Configuring WSL firewall rules](#configuring-wsl-firewall-rules)

# Prerequisites

You must be running Windows 10 (Build 22H2 and higher) or Windows 11 (Build 22H2 and higher) or Windows Server 2022 and higher to use the commands below. If you are on earlier versions please see [the manual install page](https://learn.microsoft.com/en-us/windows/wsl/install-manual). 

* The virtualization thechnology must be enabled in the computer's BIOS settings.
* Install Hyper-V by following the steps outlined in the official documentation for [Windows](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) and [Windows Server](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server)

# WSL installation

For a detailed guide on how to install Linux on Windows using WSL, you can refer to [the official Microsoft documentation](https://learn.microsoft.com/en-us/windows/wsl/install). The page provides a comprehensive overview of the available installation options, and it is recommended that you follow the steps outlined there for a complete installation.

For a more concise version of the installation procedure, the following steps are provided below.

# Install WSL command

You can now install everything you need to run WSL with a single command. Open PowerShell or Windows Command Prompt in **`administrator`** mode by right-clicking and selecting "Run as administrator", enter the following command, then restart your machine.

```powershell
wsl --install -d Ubuntu
```

Following a successful installation, it's necessary to reboot your system to ensure that the changes take effect. After rebooting, you should expect a Windows Command Prompt to automatically appear and proceed with the installation of the Ubuntu distribution. If the automatic installation didn't occur or if you prefer a different Linux distribution, please proceed to the next step to manually install your preferred Linux distribution.

# WSL shell

To enter the WSL shell from the Windows environment, execute the following command:

```powershell
wsl
```

You can exit the WSL shell into the Windows environment by executing the following command:

```bash
exit
```

# Change the default Linux distribution installed

~~By default, the installed Linux distribution will be Ubuntu. This can be changed using the **`-d`** flag.~~

* ~~To change the distribution installed, enter: **`wsl --install -d <Distribution Name>`**. Replace **`<Distribution Name>`** with the name of the distribution you would like to install.~~
* ~~To see a list of available Linux distributions available for download through the online store, enter: **`wsl --list --online`** or **`wsl -l -o`**.~~
* ~~To install additional Linux distributions after the initial install, you may also use the command: **`wsl --install -d <Distribution Name>`**.~~

If you run into an issue during the install process, check the [installation section of the troubleshooting guide](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting#installation-issues).

# Set up Linux username and password

Once the process of installing your Linux distribution with WSL is complete, open the distribution (Ubuntu by default) using the Start menu. You will be asked to create a User Name and Password for your Linux distribution.

* Unless requested differently, the username should be set to **`miscout`**.
* The password for the **`miscout`** user should be set as the default password of the **`SA`** database user.

# Update WSL

Windows Subsystem for Linux (WSL) can be updated through the Windows Update feature. To manually update your WSL version to the latest one, you can use the following command (from a Windows terminal):

```powershell
wsl --update --web-download
```

Options include:

* **`--web-download`**: Download the latest update from the GitHub rather than the Microsoft Store.

This change will take effect on the next full restart of WSL. To force a restart, please run:

```powershell
wsl --shutdown
```

# Supported WSL versions

WSL is required to be version `2.0.14` or higher.

To check which version of WSL is installed, run the following command:

```powershell
wsl --version
```

If the command doesn't output correct versions, it means that an outdated version of WSL is installed. To install a newer WSL version, you might have to update your OS.

# Configuring DNS

If DNS is not working on WSL, please follow these simple instructions.

Execute the following command (in WSL shell) to create the file **`/etc/wsl.conf`** with the proper content that ensures your DNS changes do not get overwritten:

```bash
echo -e "\n[boot]\nsystemd=true\n\n[network]\ngenerateResolvConf=false\n" | sudo tee /etc/wsl.conf
```

This example uses the IP address `8.8.8.8` for the DNS server. However, please note that it is recommended to use your own DNS server.

To get a list of available DNS servers, run the next command in a `cmd` window, and look for **DNS Servers**.

```powershell
ipconfig /all
```

Create a file **`/etc/resolv.conf`**. If it exists, delete the existing one and create this new file.
This can be done by executing the following commands:

```bash
sudo rm /etc/resolv.conf
```
```bash
echo -e "nameserver 8.8.8.8\n" | sudo tee /etc/resolv.conf
```

Run the following command to make your changes permanent.

```bash
sudo chattr +i /etc/resolv.conf
```

Exit the WSL shell by executing the following command:

```bash
exit
```

In a `cmd` window, run the following command to restart WSL:

```powershell
wsl --shutdown
```

And finally, if you have a Cisco AnyConnect VPN, run the following command in the Windows PowerShell terminal:

```powershell
Get-NetAdapter | Where-Object {$_.InterfaceDescription -Match "Cisco AnyConnect"} | Set-NetIPInterface -InterfaceMetric 6000
```

Restart WSL on the same elevated powershell, then you can open up wsl2 and it should connect to the internet.

# Update and upgrade packages

Enter the WSL shell from the Windows environment by executing the following command:

```powershell
wsl
```

It is recommended to regularly update and upgrade packages using the preferred package manager for your distribution. For Ubuntu or Debian, you can use the following command:

```bash
sudo apt update && sudo apt upgrade -y
```

Windows does not automatically update or upgrade the Linux distribution(s). Users must take control of this task and manage updates and upgrades manually.

# Configuring WSL firewall rules

Microsoft implements Firewall protocols used by Windows to maintain security and block unauthorized network traffic flowing into or out of a local device. To optimize protection for devices in your network, [configure your Windows Firewall based on best practices](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/best-practices-configuring).
