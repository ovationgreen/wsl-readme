# Apache Cassandra Installation Manual

# Table of Contents

1. [Prerequisites](#prerequisites)
2. [Update Your System](#update-your-system)
3. [Install Java](#install-java)
4. [Add the Cassandra Repository (Debian/Ubuntu only)](#add-the-cassandra-repository-debianubuntu-only)
5. [Install Apache Cassandra](#install-apache-cassandra)
6. [Start and Enable Cassandra Service](#start-and-enable-cassandra-service)
7. [Verify Cassandra Installation](#verify-cassandra-installation)
8. [Cassandra Folder Structure](#cassandra-folder-structure)
9. [Configuration and Further Steps](#configuration-and-further-steps)

# Prerequisites

Before you begin the installation process, ensure you have the following prerequisites in place:

* A Linux-based system (e.g., Debian, Ubuntu, Red Hat, CentOS)
* Root or sudo user access

# Update Your System

To start, make sure your package repository information is up to date:

For Debian/Ubuntu:

```bash
sudo apt update
```

For Red Hat/CentOS:

```bash
sudo yum update
```

# Install Java

Apache Cassandra requires Java to run. You can install OpenJDK or Oracle Java. Here's an example of how to install OpenJDK 8:

```bash
sudo apt install openjdk-8-jre
```

For Red Hat/CentOS:

```bash
sudo yum install java-1.8.0-openjdk
```

# Add the Cassandra Repository (Debian/Ubuntu only)

If you are using Debian/Ubuntu, you need to add the Apache Cassandra repository. Follow these steps:

Create a Cassandra sources list file:

Cassandra 3.11:

```bash
echo "deb https://debian.cassandra.apache.org 311x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
```

Cassandra 4.1:

```bash
echo "deb https://debian.cassandra.apache.org 41x main" | sudo tee -a /etc/apt/sources.list.d/cassandra.sources.list
```

Add the Apache Cassandra repository's GPG key:

```bash
sudo curl https://downloads.apache.org/cassandra/KEYS | sudo apt-key add -
```

# Install Apache Cassandra

Now, you can install Apache Cassandra:

For Debian/Ubuntu (after adding the repository):

```bash
sudo apt update
sudo apt install cassandra
```

For Red Hat/CentOS:

```bash
sudo yum install cassandra
```

# Start and Enable Cassandra Service

For Debian/Ubuntu:

```bash
sudo service cassandra start
```

For Red Hat/CentOS:

```bash
sudo systemctl start cassandra
```

To ensure Cassandra starts automatically on system boot:

For Debian/Ubuntu:

```bash
sudo update-rc.d cassandra defaults
```

For Red Hat/CentOS:

```bash
sudo systemctl enable cassandra
```

# Verify Cassandra Installation

You can verify that Cassandra is running by using the **`nodetool`** command:

```bash
nodetool status
```

# Cassandra Folder Structure

1. **Cassandra Root Directory:**
    - The Cassandra root directory, which contains all the Cassandra-related files and subdirectories, is usually located at **`/etc/cassandra`** for configuration files and **`/usr/share/cassandra`** for the Cassandra binary files on Debian-based systems. On Red Hat-based systems, the Cassandra root directory can be found at **`/etc/cassandra`** and **`/usr/share/cassandra`**.
2. **Configuration Files:**
    - Configuration files for Cassandra are usually stored in the **`/etc/cassandra`** directory. The primary configuration file is **`cassandra.yaml`**, and other files like **`cassandra-env.sh`**, **`cassandra-rackdc.properties`**, and **`cassandra-topology.properties`** can also be found here.
3. **Data Directories:**
    - Cassandra stores data in data directories. By default, these directories are located in **`/var/lib/cassandra/data`**. This is where Cassandra stores the actual data files.
4. **Commitlog Directory:**
    - The commitlog directory, which stores write-ahead log files, is typically located in **`/var/lib/cassandra/commitlog`**.
5. **Saved Caches Directory:**
    - Saved caches are stored in the **`/var/lib/cassandra/saved_caches`** directory. This is where Cassandra stores cache data to improve read performance.
6. **Log Files:**
    - Cassandra log files can be found in the **`/var/log/cassandra`** directory. The primary log file is **`system.log`**.
7. **Scripts and Binaries:**
    - The Cassandra binary files, including the **`cassandra`** server, can be found in the **`/usr/share/cassandra`** directory. Additionally, various scripts and utilities can be found here.
8. **Tools and Utilities:**
    - Cassandra tools and utilities, such as **`cqlsh`** (Cassandra Query Language Shell), are usually located in **`/usr/share/cassandra/tools`**.
9. **Startup Scripts:**
    - Startup scripts for Cassandra, which are used to control the service, are typically located in **`/etc/init.d`** on older systems or managed using systemd service units on newer systems. These files are named **`cassandra`**.

All these file and folder locations are based on a standard installation of Cassandra on Linux, and they may vary slightly depending on the specific Cassandra version, the Linux distribution, and any custom configurations that may have been applied during the installation process.

# Configuration and Further Steps

You have successfully installed Apache Cassandra. Further configuration and management can be done using the cqlsh command-line tool and other management tools. Refer to the official Cassandra documentation for details on configuring and managing your Cassandra cluster.

Congratulations! You now have Apache Cassandra installed and running on your Linux system. Please consult your specific Linux distribution's official documentation for any distribution-specific instructions or updates to these steps.