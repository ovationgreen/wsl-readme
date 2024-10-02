# Installing Cassandra on WSL without Internet access

The purpose of this document is to provide step-by-step guide allowing to install Cassandra 4.x on Windows Server without having access to Internet.

# Table of Contents

1. [Prerequisites](#prerequisites)
2. [WSL installation](#install-wsl)
3. [Install Ubuntu package](#install-ubuntu)
4. [Install Cassandra](#install-cassandra)

# Prerequisites

You must be running Windows Server 2022 and higher to use the steps below. If you are on earlier versions please see [the manual install page](https://learn.microsoft.com/en-us/windows/wsl/install-manual). 

* The virtualization thechnology must be enabled in the computer's BIOS settings.
* Install Hyper-V by following the steps outlined in the official documentation for [Windows](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) and [Windows Server](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-the-hyper-v-role-on-windows-server)

# Install WSL

To turn on WSL there must be executed the following commands:
```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
* Download the following file: [wsl_update_x64.msi](https://emerson.sharepoint.com/:u:/r/sites/OvationGreenSCADA/Ovation%20Green%20SCADA%20binaries/Cassandra-Linux/Offline/wsl_update_x64.msi?csf=1&web=1&e=LP5ZDK)
* Run downloaded binary
* Following a successful installation, it's necessary to reboot your system to ensure that the changes take effect.
 
# Install Ubuntu

The following steps allow installing Ubuntu on WSL in offline mode.
* Download Ubuntu offline installer: [Ubuntu-setup.zip](https://emerson.sharepoint.com/:u:/r/sites/OvationGreenSCADA/Ovation%20Green%20SCADA%20binaries/Cassandra-Linux/Offline/Ubuntu-setup.zip?csf=1&web=1&e=9PXlRX)
* Extract content of archive
* Run the following binary: 
```powershell
Ubuntu.exe
```

After installation has been finished, you should expect an Ubuntu shell window opened. 

# Install Cassandra

Cassandra and all dependent libraries for Ubuntu is located in file [cassandra-offline.zip](https://emerson.sharepoint.com/:u:/r/sites/OvationGreenSCADA/Ovation%20Green%20SCADA%20binaries/Cassandra-Linux/Offline/cassandra-offline.zip?csf=1&web=1&e=1HxBJk). It is important to know that Cassandra and all dependencies are suitable for Ubuntu package described in chapter [Install Ubuntu package](#install-ubuntu).
* Extract content of .ZIP file **`cassandra-offline.zip`** to some folder on drive C: (for example **`c:\cassandra`**).
* From Linux on WSL that folder is accessible at **`/mnt/c/cassandra`**
* Run the following command:
```powershell
cd /mnt/c/cassandra
sudo dpkg -i *
sudo dpkg -i *
```
Command **`sudo dpkg -i *`** must be executed twice because after first time there still available installation errors. 

After installation has been finished follow Cassandra configuration steps desribed in section [Configuring Cassandra on WSL](cassandra-on-wsl/README.md).
After configuration is done, start Cassandra service by executing
```powershell
sudo service cassandra start
```
and make sure it is running
```powershell
sudo service cassandra status
```

  

