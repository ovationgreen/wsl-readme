# Docker Overview

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code, you can significantly reduce the delay between writing code and running it in production.

# Purpose

The purpose of this document is to guide users through the installation process of Docker on a Windows Server environment. This guide aims to provide clear and step-by-step instructions to help users install Docker on their Windows Server, ensuring a smooth and successful setup.

This document primarily concentrates on setting up Docker Desktop in a Windows Server environment. For instructions on how to install and configure containers on a Windows Server, please refer to the [official documentation](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce).

# Table of Contents

1. [Installing](#installing)
2. [Links](#links)

# Installing

Begin by downloading [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop). Throughout the installation, select the `WSL2` option, and proceed with the installation. You'll be prompted to log out during the install process; please log out and then log in again.

# Start Docker Desktop

Docker Desktop does not start automatically after installation. To start Docker Desktop:

1. Search for Docker, and select **Docker Desktop** in the search results.
2. The Docker menu ( whale menu ) displays the Docker Subscription Service Agreement.
3. Select **Accept** to continue. Docker Desktop starts after you accept the terms.

# Links

* [Docker](https://www.docker.com)
* [Docker Desktop](https://www.docker.com/products/docker-desktop)
* [Install Docker Desktop on Windows](https://docs.docker.com/desktop/install/windows-install)
* [Containers on Windows](https://learn.microsoft.com/en-us/virtualization/windowscontainers)