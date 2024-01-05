# Performance Comparison

The purpose of this section is to provide a comparison of various Cassandra deployment types, making it simpler for users to make an informed choice between them.

# Testing Methodology

All test were performed using [Cassandra Stress](https://cassandra.apache.org/doc/stable/cassandra/tools/cassandra_stress.html).

The **`cassandra-stress`** tool was used to benchmark and load-test a Cassandra standalone instance and a Cassandra cluster. It supports testing arbitrary CQL tables and queries, allowing users to benchmark their own data model.

The primary metric for all tests is the **`Row rate`**, which represents the number of rows that can be stored or read per second.

Each test can be compared against any other test conducted on the same machine. Comparisons against tests on different machines are feasible when the hardware configurations are identical.

# Testing Environments

Tests were conducted on a range of machines with variations in operating systems and hardware configurations.

* Workstation
    - **`OS`**: Windows 11 Enterprise 22H2
    - **`Processor`**: 12th Gen Intel(R) Core(TM) i9-12900K   3.19 GHz
    - **`Installed RAM`**: 64,0 GB (63,8 GB usable)
* Server
    - **`OS`**: Windows Server 2022 Standard 21H2
    - **`Processor`**: Intel(R) Xeon(R) CPU E5-2620 v3 @ 2.40GHz   2.40 GHz
    - **`Installed RAM`**: 8.00 GB
* Linux
    - **`OS`**:
    - **`Processor`**: Intel(R) Xeon(R) CPU E5-2620 v3 @ 2.40GHz   2.40 GHz
    - **`Installed RAM`**:
* Server 2
    - **`OS`**: Windows Server 2022 Standard 21H2
    - **`Processor`**: Intel(R) Xeon(R) CPU E5-2690 v3 @ 2.60GHz   2.60 GHz  (4 processors)
    - **`Installed RAM`**: 16.0 GB

# Testing Conditions

The **`cassandra-stress`** tool was utilized to generate a dataset consisting of **`500,000,000`** rows before executing the tests. The database size containing the testing data was approximately **`500 GB`**. The number of threads used was restricted to **`16`** threads. The tests encompassed write-only, read-only, and mixed workloads involving standard data.

The following Cassandra deployments were subject to comparison:

* **`Windows`**: Cassandra version for Windows
* **`WSL`**: Cassandra running on Windows Subsystem for Linux (WSL)
* **`WSL (windows drive)`**: Cassandra running on Windows Subsystem for Linux (WSL) with data storage configured to use a Windows drive.
* **`Ubuntu`**: Ubuntu distribution operating on comparable hardware.
* **`Docker`**: Cassandra running within a Docker container.

In all the tests, Cassandra version **`3.11.16`** was utilized.

# Testing Commands

The following commands were employed to generate the testing results:

```shell
cassandra-stress write n=500000000 -node <ip> -rate threads=16
cassandra-stress read  n=500000000 -node <ip> -rate threads=16
cassandra-stress mixed n=500000000 -node <ip> -rate threads=16
```

# Testing Results for Workstation

| Deployment          | Write (row/s) | Read (row/s) | Mixed (row/s) |
| ------------------- | ------------- | ------------ | ------------- |
| Windows             | 11 183        | 11 477       | 11 582        |
| WSL                 | 60 263        | 54 503       | 53 323        |
| WSL (windows drive) | 66 391        | 63 318       | 57 593        |
| Docker              | -             | -            | -             |

# Testing Results for Server

| Deployment          | Write (row/s) | Read (row/s) | Mixed (row/s) |
| ------------------- | ------------- | ------------ | ------------- |
| Windows             | 4 950         | 4 623        | 4 630         |
| Ubuntu              | 9 710         | 8 888        | 8 797         |

# Testing Results for Linux

| Deployment          | Write (row/s) | Read (row/s) | Mixed (row/s) |
| ------------------- | ------------- | ------------ | ------------- |
| Ubuntu              | 9 710         | 8 888        | 8 797         |
| Docker              | -             | -            | -             |

# Testing Results for Server 2

| Deployment          | Write (row/s) | Read (row/s) | Mixed (row/s) |
| ------------------- | ------------- | ------------ | ------------- |
| Windows             | 14 989        | 11 230       | 10 453        |
| WSL (windows drive) | 14 461        | 15 384       | 12 635        |
| Docker              | 4 126         | 4 074        | 3 094         |

# Observations

During the test executions, the following observations were noted:

1. Cassandra on a Linux environment demonstrates significantly improved performance compared to a pure Windows installation. However, it's important to note that the CPU load is also proportionally higher in the Linux environment.

2. Cassandra on Windows Subsystem for Linux (WSL) exhibits improved performance when configured to utilize a Windows drive.

3. Running Cassandra inside a Docker container can limit performance by a factor of 4.
