---
title: Install and upgrade the ACS Kubernetes Connector
sidebar_label: Installation
description: "Install or upgrade the ACS Kubernetes Connector by deploying the plugin directory to your OpCon environment."
tags:
  - Procedural
  - System Administrator
  - Agents
  - Installation
---

# Install and upgrade the ACS Kubernetes Connector

**Theme:** Configure  
**Who Is It For?** System Administrator

## What is it?

The ACS Kubernetes Connector is distributed as a plugin directory that you deploy into your OpCon environment. Installation requires copying the plugin files to the correct location and restarting the relevant services.

- Use the installation procedure when setting up the connector in a new OpCon environment
- Use the upgrade procedure when a new connector version is available and you need to apply it to an existing installation

## Installation

Download the ACS KubernetesJob software from the SMA FTP site. The files are located at `/OpCon Releases/Integrations/KubernetesJob/`. Select the required version and download the archive.

To install the connector, complete the following steps:

1. Unzip the `KubernetesJob.zip` file.
2. Copy the `KubernetesJob` directory to the correct location for your deployment type:

   | Deployment | Destination directory |
   |---|---|
   | On-premises | `\SAM\plugins\` |
   | Cloud | `\Relay\plugins\` |

3. Restart the services for your deployment type:

   | Deployment | Services to restart |
   |---|---|
   | On-premises | **SMA OpCon Services Manager** and **SMA OpCon RestAPI** |
   | Cloud | **SMA OpCon Relay** |

The connector is registered with OpCon after the services start.

## Upgrade

Download the ACS KubernetesJob upgrade package from the SMA FTP site at `/OpCon Releases/Integrations/KubernetesJob/`.

To upgrade the connector, complete the following steps:

1. Unzip the `KubernetesJob.zip` file.
2. Stop the services for your deployment type:

   | Deployment | Services to stop |
   |---|---|
   | On-premises | **SMA OpCon Services Manager** and **SMA OpCon RestAPI** |
   | Cloud | **SMA OpCon Relay** |

3. Copy the `KubernetesJob` directory to the correct location, overwriting the existing files:

   | Deployment | Destination directory |
   |---|---|
   | On-premises | `\SAM\plugins\` |
   | Cloud | `\Relay\plugins\` |

4. Restart the services:

   | Deployment | Services to restart |
   |---|---|
   | On-premises | **SMA OpCon Services Manager** and **SMA OpCon RestAPI** |
   | Cloud | **SMA OpCon Relay** |

The upgraded connector is active after the services start.

## FAQs

**Where do I find the connector download?**  
The connector is available on the SMA FTP site at `/OpCon Releases/Integrations/KubernetesJob/`. Contact SMA Technologies support if you do not have FTP access.

**Do I need to stop services before installing for the first time?**  
No. A fresh installation does not require stopping services first. Only upgrades require stopping services before replacing the plugin files.

**What is the difference between the on-premises and cloud installation paths?**  
On-premises environments use the SAM plugin directory because the connector communicates directly with OpCon. Cloud environments use the Relay plugin directory because the ACS connector communicates with OpCon through the Relay service.

## Glossary

**Plugin directory** — The file system folder where OpCon loads connector plugin assemblies at startup. The `\SAM\plugins\` path is used for on-premises deployments; `\Relay\plugins\` is used for cloud deployments.

**SMA OpCon Relay** — The service that provides the communication bridge between cloud-hosted OpCon and on-premises or remote agents and connectors.
