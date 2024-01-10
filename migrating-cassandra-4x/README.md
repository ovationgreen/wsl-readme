# Migration

This scenario is about migrating (upgrading) an existing Cassandra 3.x to Cassandra 4.x.

# Prerequisites

It is assumed that an existing Cassandra 3.x installation is present, and it needs to be migrated to Cassandra 4.x.

WSL with Cassandra 4.x must be installed and configured on the target machine.

# Limitations

This specific manual focuses solely on migrating a standalone Cassandra instance; clustered instances should be migrated by following another, more specific manual.

# Changing the location of directories

The following properties in the YAML configuration file must be changed to reference mounted Windows directories:

* data_file_directories
* commitlog_directory
* saved_caches_directory
* hints_directory

# Copying existing database

The contents of the `data` folder of an existing Cassandra 3.x installation must be copied to the Windows directory mounted in WSL. Please ensure that all four properties from the previous section have the correct values and are referencing the copied folders. After migration, the data folders will be incompatible with Cassandra 3.x.

# Starting Cassandra

When the correct folders have been specified, and all the data has been copied, it is time to start the Cassandra service on WSL. It will initiate the migration process during startup and make the data available after full initialization.