---
sidebar_label: 'Release notes'
title: ACS Kubernetes Connector release notes
description: "Version history and change details for the ACS Kubernetes Connector, including new features, improvements, and bug fixes."
tags:
  - Reference
  - System Administrator
  - Automation Engineer
  - Agents
---

# ACS Kubernetes Connector release notes

## 26

### 26.0.4

2026 July

#### What's new

:eight_spoked_asterisk: **CON-1868**: Add RestartPolicy option. 
:eight_spoked_asterisk: **CON-1953**: Add BackOffLimits option. 

### 26.0.3

2026 June

#### What's new

:eight_spoked_asterisk: **CON-1722**: Support definition of multiple volume mounts. 

:eight_spoked_asterisk: **CON-1727**: Support definition of environment variables. 

### 26.0.2

2026 May

#### What's new

:eight_spoked_asterisk: **CON-1507**: Added the capability to optionally define a volume mount when defining a Kubernetes Job. 

### 26.0.1

2026 April

#### What's new

:eight_spoked_asterisk: **CON-1156**: Changed the command and argument separator from space to comma, allowing commands and arguments that contain spaces to be passed correctly to the container.

:eight_spoked_asterisk: **CON-1197**: Added **Name Space** field to the task definition, allowing jobs to target a specific Kubernetes namespace.

:eight_spoked_asterisk: **CON-1217**: Separated job submission from monitoring, so OpCon monitors the Kubernetes job for completion as a running job.

:eight_spoked_asterisk: **CON-1218**: Added **Resources** section (requests and limits) to the Kubernetes Job YAML definition, allowing CPU and memory constraints to be specified per job.

:eight_spoked_asterisk: **CON-1219**: Implemented a job log cleanup check after task completion, which removes old log files from the connector's log folder.

#### Why this matters

These updates improve the reliability and configurability of Kubernetes job runs from OpCon. The separator change fixes a class of command-line failures for images that require space-containing arguments. The resource controls allow operations teams to prevent runaway pods from consuming excessive cluster resources. Separating submission from monitoring improves visibility into long-running jobs by enabling standard OpCon job status monitoring throughout the pod lifecycle.

### 26.0.0

2026 February

Initial release of the ACS Kubernetes Connector.
