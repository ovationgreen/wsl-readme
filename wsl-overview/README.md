# Overview

Starting from version 4.0, Cassandra necessitates a Linux environment for its operation. The objective of this documentation is to elucidate the process of installing Cassandra on WSL, optimizing its configuration, and providing guidance on its ongoing maintenance.

# Legacy solution

Historically, Cassandra was part of the Ovation Green installation package intended to work on the Windows platform. It was installed together with Ovation Green and required only a set of TCP ports to be opened in the firewall, especially if a connection through LAN was necessary or in the case of a cluster solution.

# Moving forward

Starting now, Cassandra will no longer be included in the Ovation Green installation package for Windows. Instead, it will be installed and configured on WSL manually by following this guide. In the future, a preinstalled and preconfigured distribution can be created for WSL to simplify this somewhat tedious process.

# Prerequisites

You must be running Windows 10 (Build 22H2 and higher) or Windows 11 (Build 22H2 and higher) or Windows Server 2022 and higher.
* The virtualization thechnology must be enabled in the computer's BIOS settings.
* In the case of a virtual machine, nested virtualization must be enabled.
* Microsoft Hyper-V must be installed.

# Windows Subsystem for Linux (WSL)

The Windows Subsystem for Linux (WSL) enables us to run a GNU/Linux environment, complete with a wide range of command-line tools, utilities, and applications, directly on Windows. By using WSL, we eliminate the need for a full-fledged Linux distribution for Cassandra 4.x and can maintain the management of Cassandra's database files on the Windows platform.

# WSL distro

Ubuntu has been chosen as the default distribution for WSL. In addition to `Cassandra`, we also install the `openjdk-8-jre` and `mc` packages on the distribution.

# Cassandara on WSL

Cassandra is installed and configured on WSL the same way it would be on any other Linux distribution. There are only minor configuration changes related to file storage. By default, Windows drives are visible in WSL as mounts, and we configure Cassandra to use such a mount for its database directory.

# Accessing Cassandra from Windows (localhost)

If you are running Cassandra on the same machine as Ovation Green, you can access it from a Windows using localhost (just like you normally would).

# Accessing Cassandra on WSL from the local area network (LAN)

WSL 2 has a virtualized ethernet adapter with its own unique IP address. Currently, to enable this workflow you will need to go through the same steps as you would for a regular virtual machine. We utilize the Netsh interface portproxy commands to configure port forwarding between the Windows host machine and the WSL distribution.

# Windows firewall

All used ports (`7000`, `7001`, `7199`, `9042`, `9160`) must be added to the Windows firewall's rules to allow both inbound and outbound connections.
