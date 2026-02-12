# ACS KubernetesJob Connector

The ACS Kubernetes Job submits requests to a Kubernetes environment to execute a command within a container (pod). The Kubernetes environment will spin up the container (pod) and execute the task. It is possible to request Kubernetes to execute this task within multiple containers (pods) and also specify how many of the containers (pods) may execute in parallel. Once the execution is complete, the ACS KubernetesJob requests the job log from all containers (pods) and consolidates these outputs into a single OpCon job log. 

The Kubernetes Job ensures that the job environment is cleaned up correctly following the job execution. 

![Overview](../static/img/overview.png)

The ACS KubernetesJob implementation uses the KubernetesClient library to provide the connection between ACS and the Kubernetes Cluster. The KubernetesClient submits the requests, monitors them. Upon completion ACS requests the KubernetesClient to retrieve the job log from the containers (pods) and then cleanup. Then ACS formats a single OpCon job log containing all the job logs from the containers (pods).