# Example: Developer documentation (architecture)

```markdown
---
outline: [2, 3]
description: Core architecture of Olares deployment across native system layer, Kubernetes orchestration and containerized services.
---

# Olares installation architecture

This document provides a high-level overview of the Olares installation process, focusing on its overall architecture and core components. It is intended for system administrators and developers who need a foundational understanding of how Olares operates and is installed.

## Three layers of Olares installation

The Olares installation is structured into three key layers:

- **Native layer**: Manages Linux system configurations and installs essential environment dependencies.
- **Container orchestration layer**: Deploys the Kubernetes cluster to enable automated service management and scaling.
- **Containerization layer**: Launches containerized core system services and user applications, providing the final runtime environment.

The installation process is managed by the `olares-cli` tool. This command-line tool orchestrates the installation, configuration, and lifecycle management of all components.

![Install arch](/images/developer/install/olares-install.png)

::: tip
To understand the detailed installation process phase-by-phase, refer to [Olares installation breakdown](installation-process.md).
:::

## Native layer

The Olares installation process begins at the native layer, ensuring that the underlying Linux environment supports distributed storage, container runtimes, and Kubernetes cluster management.

This layer's configuration includes core Linux system settings, file system initialization, container runtime installation, and deployment of critical system services.

### Environment configuration

The installation first configures the basic Linux installation environment. This includes setting up Domain Name System (DNS), Secure Shell (SSH), and Network Time Protocol (NTP) services to ensure time synchronization and remote management capabilities.

Additionally, necessary dependencies such as the GNU Compiler Collection (GCC) and Network Tools (net-tools) are installed to ensure a robust runtime environment.

### File system configuration

The root file system (rootfs) is used to store and access system core components and user data. Olares supports the following two file systems based on deployment needs:

- **LocalFS** (default): Uses the local Linux disk for storage. It is ideal for single-node deployments that require high data throughput without the need for network sharing.

- **JuiceFS**: Provides a distributed file system for multi-node cluster.

  :::tip Enable JuiceFS
  JuiceFS and MinIO are not installed by default. To enable them, set the necessary [environment variables](environment-variables.md#juicefs).
  :::

## Container orchestration layer

The container orchestration layer integrates system components into an efficient runtime environment using Kubernetes.

### Roles of Kubernetes

Kubernetes serves as the backbone of the container orchestration layer, providing automated deployment, operation, scaling, and management of multi-component services.

## Learn more

- [Olares installation breakdown](installation-process.md)
- [Olares CLI](../install/cli/olares-cli.md)
```
