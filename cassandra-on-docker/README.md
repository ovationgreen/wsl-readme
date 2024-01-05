# Apache Cassandra Installation Manual

This section delineates the process of installing Cassandra on a Docker instance.

# Table of Contents

1. [Prerequisites](#prerequisites)
2. [Get Cassandra using Docker](#get-cassandra-using-docker)
3. [Links](#links)

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

# 

# Links

* [Cassandra Official Images](https://hub.docker.com/_/cassandra)
* [Quick Start Guide](https://cassandra.apache.org/_/quickstart.html)
* [Getting Started](https://cassandra.apache.org/doc/4.1/cassandra/getting_started/installing.html)