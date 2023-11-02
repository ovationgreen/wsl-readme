# Apache Cassandra Installation Manual

# Table of Contents

1. [Prerequisites](#)
2. [Update Your System](#)
3. [Install Java](#)
4. [Add the Cassandra Repository (Debian/Ubuntu only)](#)
5. [Install Apache Cassandra](#)
6. [Start and Enable Cassandra Service](#)
7. [Verify Cassandra Installation](#)
8. [Configuration and Further Steps](#)

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