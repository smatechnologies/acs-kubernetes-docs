---
title: Define a Kubernetes job task
sidebar_label: Task definition
description: "Define a Kubernetes job task in OpCon to submit a containerized command to a Kubernetes cluster through the ACS Kubernetes Connector."
tags:
  - Procedural
  - Automation Engineer
  - Jobs
  - Agents
---

# Define a Kubernetes job task

**Theme:** Configure  
**Who Is It For?** Automation Engineer

## What is it?

A Kubernetes job task tells OpCon what container image to run, what command and arguments to pass to it, how many pods to spin up, and what resource limits to apply. When OpCon runs the job, the connector submits these parameters to the Kubernetes cluster.

- Use this procedure when you need to schedule a containerized workload through OpCon
- Use this procedure when configuring resource constraints for jobs that run in a shared Kubernetes cluster

The Kubernetes Connector supports the following task type:

| Task type | Description |
|---|---|
| Job | Runs a command within a container in a Kubernetes cluster |

## Define a Job task

**Prerequisite:** The Kubernetes agent must be defined and communicating before a job task can be submitted. See [Agent definition](./agent-definition.md).

To define a Kubernetes job task, complete the following steps:

1. In Solution Manager, select **Library**.
2. From the **Administration** menu, select **Master Jobs**.
3. Select **+Add**.
4. In the **Schedule** field, select the schedule name from the list.
5. In the **Name** field, enter a unique name for the job within the schedule.
6. In the **Job Type** field, select **Kubernetes Job** from the list.
7. In the **Task Type** field, select **Job** from the list.
8. Select the **Task Details** button.
9. In the **Integration Selection** section, select the Kubernetes agent previously defined.
10. In the **Task Configuration** section, complete the following fields:

    | Field | Description | Required | Default |
    |---|---|---|---|
    | **Environment Variables** | Multiple environment variables can be added by selecting the **+ AddItem** button. Each variable has a **Name** and a **Value**. To read the value from a Kubernetes Secret instead, select the **Value From** option and enter the **Key** within the secret and the **Name** of the secret. When **Value From** is selected, the **Value** field is not required. A value cannot contain `=` or `;` | No | |
    | **Image** | The Docker Registry image that provides the runtime environment for the command | Yes | |
    | **Name Space** | The Kubernetes namespace to run the job in | Yes | `default` |
    | **Job Name** | The name assigned to the Kubernetes job object | Yes | |
    | **Container Name** | The name assigned to the container when the image runs | Yes | |
    | **Command** | The command to run inside the container. Separate multiple values with a comma (`,`); a value cannot contain a comma | Yes | |
    | **Arguments** | The arguments to pass to the command. Separate multiple values with a comma (`,`); a value cannot contain a comma | No | |
    | **Volume Mounts** | Optional information about a volume that should be mounted for the task to process. Add definitions by selecting the **+ AddItem** button. Enter the **Name**, the **Mount Path**, the **Claim Name** or **Secret Name**, and select the **Read Only** option if the volume is read only | No | |
    | **Resources** | The CPU and memory requests and limits applied to each pod, set in the four fields that follow | Yes | |
    | **Request CPU** | The initial CPU allocation guaranteed to each pod | Yes | `250m` |
    | **Request Memory** | The initial memory allocation guaranteed to each pod | Yes | `512Mi` |
    | **Limit CPU** | The maximum CPU each pod may consume | Yes | `500m` |
    | **Limit Memory** | The maximum memory each pod may consume | Yes | `1Gi` |
    | **Pods to Complete** | The number of pod runs the job needs. The job ends when the number of pods that have succeeded or failed reaches this value, and finishes successfully only if all of them succeeded | Yes | `1` |
    | **Parallel Executions** | The number of pods that may run concurrently | Yes | `1` |
    | **Restart Policy** | The restart policy to set for the job: **Never** or **OnFailure** | Yes | |
    | **BackOffLimits** | The number of retries Kubernetes allows on failure. With **Restart Policy** set to **Never**, the first failed pod fails the job and the connector removes the Kubernetes job before it can retry. Retries happen with **OnFailure**, where Kubernetes restarts the container within the same pod | Yes | `6` |


11. Select the **Save** button. The job is added to the schedule.

## Killing a job

:::caution
Killing the job in OpCon does not delete the Kubernetes job. Its pods keep running in the cluster, and a later run with the same **Job Name** in that namespace fails until the job is deleted. Delete the job in the cluster, for example with `kubectl delete job <name> -n <namespace>`.
:::

## Job log

The job log contains the job settings, the environment variables with their values, and the output of each pod. Environment variables entered as plain values appear in the job log as entered, so use **Value From** for sensitive values.

## FAQs

**How do I pass multiple commands or arguments?**  
Separate multiple values with a comma (`,`). For example, to pass two arguments, enter `--config,/etc/app/config.yaml` in the **Arguments** field.

**What is the difference between Pods to Complete and Parallel Executions?**  
**Pods to Complete** sets the total number of pod runs the job needs. **Parallel Executions** sets how many of those pods can run at the same time. For example, setting **Pods to Complete** to `4` and **Parallel Executions** to `2` runs two pods at a time until four have finished. The job finishes successfully only if all four succeeded.

**What happens if a pod exceeds its CPU or memory limit?**  
Kubernetes terminates any pod that exceeds its memory limit. CPU throttling applies when a pod exceeds its CPU limit. Set limits high enough to avoid unexpected pod terminations.

**Can I use OpCon global properties in task fields?**  
Yes. Global properties using the `[[property_name]]` token syntax are supported in all task configuration fields.

## Glossary

**Image** — A packaged container image stored in a Docker Registry that defines the runtime environment and application code for the pod.

**Namespace** — A Kubernetes isolation boundary that logically separates workloads within a cluster. Jobs submitted to a namespace are only visible to and affected by resources within that namespace.

**Pods to Complete** — The number of pod runs the job needs. OpCon waits until this many pods have finished, and marks the job complete only if all of them succeeded.

**Resource requests** — The minimum CPU and memory that Kubernetes guarantees to a pod. The cluster scheduler only places a pod on a node that has at least this much capacity available.

**Resource limits** — The maximum CPU and memory a pod may consume. Kubernetes enforces limits by throttling CPU and terminating pods that exceed memory limits.
