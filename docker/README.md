# Docker Overview

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code, you can significantly reduce the delay between writing code and running it in production.

# Purpose

The purpose of this document is to guide users through the installation process of Docker on a Windows Server environment. This guide aims to provide clear and step-by-step instructions to help users install Docker on their Windows Server, ensuring a smooth and successful setup.

This document primarily concentrates on setting up Docker in a Windows Server environment. For Windows 10/11 and advanced steps, please refer to the [official documentation](https://learn.microsoft.com/en-us/virtualization/windowscontainers/quick-start/set-up-environment?tabs=dockerce).

# Table of Contents

1. [Installing](#installing)
2. [Links](#links)

# Installing

Docker Community Edition (CE) provides a standard runtime environment for containers with a common API and command-line interface (CLI). It is managed by the open source community as part of the [Moby Project](https://mobyproject.org).

To get started with Docker on Windows Server Miscrosoft has created [a powershell script](https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1) which configures your environment to enable container-related OS features and install the Docker runtime.

```PowerShell
Invoke-WebRequest -UseBasicParsing "https://raw.githubusercontent.com/microsoft/Windows-Containers/Main/helpful_tools/Install-DockerCE/install-docker-ce.ps1" -o install-docker-ce.ps1
.\install-docker-ce.ps1
```

During the installation process, the system will reboot automatically and resume the installation process afterward.

For more configuration details, see [Docker Engine on Windows](https://learn.microsoft.com/en-us/virtualization/windowscontainers/manage-docker/configure-docker-daemon).

# Links

* [Docker](https://www.docker.com)
* [Containers on Windows](https://learn.microsoft.com/en-us/virtualization/windowscontainers)