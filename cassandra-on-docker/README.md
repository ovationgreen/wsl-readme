# Apache Cassandra Installation Manual

This section delineates the process of installing Cassandra on a Docker instance.

# Table of Contents

1. [Prerequisites](#prerequisites)
2. [Get Cassandra using Docker](#get-cassandra-using-docker)
3. [Start Cassandra](#start-cassandra)
4. [Links](#links)

# Prerequisites

Before initiating the installation process, ensure that Docker is installed. You’ll need to have Docker Desktop for Windows, or similar software installed on your computer.

# Get Cassandra using Docker

Pull the docker image. For the version 3.11, use:

```shell
docker pull cassandra:3.11
```

For the latest image, use:

```shell
docker pull cassandra:latest
```

All available Cassandra images can be found on the [official Cassandra Images page](https://hub.docker.com/_/cassandra).

# Start Cassandra

Inside Docker Desktop, navigate to the **Images** section, and click the **Run** button.

A **Run a new container** dialog will appear with an **Optional settings** section. Expand the **Optional settings** section and enter an appropriate container name. Ensure that host ports are entered the same as the default values.

In the **Volumes** section, select the **Host path** option to determine the location of Cassandra's database on the Windows machine. In the corresponding **Container path**, enter the following value:

```
/var/lib/cassandra
```

Click the **`Run`** button to generate a container from the image. The new container will now be accessible in the **Containers** section within Docker Desktop.

# Links

* [Cassandra Official Images](https://hub.docker.com/_/cassandra)
* [Quick Start Guide](https://cassandra.apache.org/_/quickstart.html)
* [Getting Started](https://cassandra.apache.org/doc/4.1/cassandra/getting_started/installing.html)