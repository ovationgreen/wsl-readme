# Configuring Cassandra

This section provides an overview of the steps for configuring Cassandra on a Linux instance, whether it's running on Windows Subsystem for Linux (WSL), Docker, or a traditional Linux distribution.

# Table of Contents

1. [Overview](#overview)
2. [Main runtime properties](#main-runtime-properties)
3. [Changing the location of directories](#changing-the-location-of-directories)
4. [Cassandra directories on WSL](#cassandra-directories-on-wsl)
5. [Environment variables](#environment-variables)
6. [Logging](#logging)
7. [IP addresses](#ip-addresses)
8. [Properties](#properties)

# Overview

The Cassandra configuration files location varies, depending on the type of installation:

* docker: **`/etc/cassandra`** directory
* package: **`/etc/cassandra`** directory

Cassandra’s default configuration file, **`cassandra.yaml`**, is sufficient to explore a simple single-node **`cluster`**. However, anything beyond running a single-node cluster locally requires additional configuration to various Cassandra configuration files. Some examples that require non-default configuration are deploying a multi-node cluster or using clients that are not running on a cluster node.

* **`cassandra.yaml`**: the main configuration file for Cassandra
* **`cassandra-env.sh`**: environment variables can be set
* **`cassandra-rackdc.properties`** OR **`cassandra-topology.properties`**: set rack and datacenter information for a cluster
* **`logback.xml`**: logging configuration including logging levels
* **`jvm-*`**: a number of JVM configuration files for both the server and clients
* **`commitlog_archiving.properties`**: set archiving parameters for the commitlog

The sample configuration files can also be found in **`./conf`**:
* **`cqlshrc.sample`**: how the CQL shell, cqlsh, can be configured

# Main runtime properties

Configuring Cassandra is done by setting yaml properties in the **`cassandra.yaml`** file. At a minimum you should consider setting the following properties:

* **`cluster_name`**: Set the name of your cluster.
* **`seeds`**: A comma separated list of the IP addresses of your cluster seed nodes.
* **`storage_port`**: Check that you don’t have the default port of 7000 blocked by a firewall.
* **`listen_address`**: The **`listen address`** is the IP address of a node that allows it to communicate with other nodes in the cluster. Set to localhost by default. Alternatively, you can set **`listen_interface`** to tell Cassandra which interface to use, and consecutively which address to use. Set one property, not both.
* **`rpc_address`**: The address or interface to bind the Thrift RPC service and native transport server to.
* **`native_transport_port`**: Check that you don’t have the default port of 9042 blocked by a firewall, so that clients like cqlsh can communicate with Cassandra on this port.

# Changing the location of directories

The following yaml properties control the location of directories:

* **`data_file_directories`**: One or more directories where data files, like **`SSTables`** are located.
* **`commitlog_directory`**: The directory where commitlog files are located.
* **`saved_caches_directory`**: The directory where saved caches are located.
* **`hints_directory`**: The directory where **`hints`** are located.

For performance reasons, if you have multiple disks, consider putting commitlog and data files on different disks.

# Cassandra directories on WSL

When running Cassandra on Windows Subsystem for Linux (WSL), it's important to reconfigure Cassandra to utilize Windows directories for improved ease of use and performance.

To access drive **`C:`** on a Windows file system within WSL, you must use the **`/mnt/c/`** file path.

# Environment variables

JVM-level settings such as heap size can be set in **`cassandra-env.sh`**. You can add any additional JVM command line argument to the **`JVM_OPTS`** environment variable; when Cassandra starts, these arguments will be passed to the JVM.

# Logging

The default logger is logback. By default it will log:

* **INFO** level in **`system.log`**
* **DEBUG** level in **`debug.log`**

When running in the foreground, it will also log at INFO level to the console. You can change logging properties by editing **`logback.xml`** or by running the nodetool setlogginglevel command.

# IP addresses

When Cassandra and Ovation Green SCADA are installed on separate machines, it's essential to modify the IP address properties within the **`cassandra.yaml`** file to reflect the external IP address. This adjustment is crucial to establish the required connectivity and communication between the two systems. The same procedure applies when Cassandra needs to be part of a cluster.

To find the correct IP address, execute the following command:

```shell
ip address
```

The found external IP address must be specified in the following properties within the **`cassandra.yaml`** file:
* **`seeds`**: Cassandra nodes use this list of hosts to find each other and learn the topology of the ring.
* **`listen_address`**: Address or interface to bind to and tell other Cassandra nodes to connect to.
* **`rpc_address`**: The address or interface to bind the Thrift RPC service and native transport server to.

# Properties

The following properties, which are related to buffer sizes and timeouts, should have their values increased if they are currently set lower:
* **`num_tokens`**: `256` (`16` by default)
* **`commitlog_segment_size_in_mb`**: `64` (`32` by default)
* **`read_request_timeout_in_ms`**: `60000` (`5000` by default)
* **`write_request_timeout_in_ms`**: `20000` (`2000` by default)
* **`enable_user_defined_functions`**: `true` (`false` by default)
* **`enable_scripted_user_defined_functions`**: `true` (`false` by default)
* **`batch_size_warn_threshold_in_kb`**: `5000` (`5` by default)
* **`batch_size_fail_threshold_in_kb`**: `500000` (`50` by default)
* **`materialized_views_enabled`**: `true` (`false` by default)
