# Agent Definition

All definitions can only be performed using Solution Manager.

Once the sma.acs.KubernetesJob plugin has been registered with the OpCon system, it will be possible to perform agent definitions.

The .kube/config associated with the Kubernetes cluster connectivity, should be saved as a KubernetesJob script.

## Defining KubernetesJob Scripts

The ACS KubernetesJob implementation uses a script to provide .kube/config file that the connection requires.

Use the created .kube/config to provide the contents of the script.

Using Solution Manager
- Select **Library**.
- Select **Scripts**.
- Select **Script Types** from the upper right hand corner. 
    - Select **+Add**
    - In the ***Name*** field enter **KubernetesJob**.
    - In the ***File Extension field*** enter **txt**.
    - In the ***Description*** field enter **Used for ACS KubernetesJob Integration**.
    - Select Save.
- Select **Script Runners** from the upper right hand corner. 
    - Select **+Add**
    - In the ***Name*** field enter **KubernetesJob**.
    - In the ***OS*** field select **KubernetesJob** from the drop-down list.
    - In the ***Type*** field select **KubernetesJob** from the drop-down list.
    - In the ***Command*** field enter **cmd.exe /c**.
    - Select Save.
- Select **Scripts** from the upper right hand corner.
    - Create the Connector.config script.
    - Select **+Add**.
    - In the ***Name*** field enter a name for the script. It is suggested using the proposed agent name and append **_config_** to the name. 
    - In the ***Type*** field select **KubernetesJob** from the drop-down list.
    - Assign the required roles.
    - In the ***Script*** paste the contents of the **.kube/config** file.
    - Select Save.

Example config file

```
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: 
    *************
    server: https://kubernetes.docker.internal:6443
  name: docker-desktop
contexts:
- context:
    cluster: docker-desktop
    user: docker-desktop
  name: docker-desktop
current-context: docker-desktop
kind: Config
users:
- name: docker-desktop
  user:
    client-certificate-data: 
    *************
    client-key-data: 
    *************
```

## Defining ACS KubernetesJob Agent

This is done by adding a new ACS KubernetesJob Agent definition using Solution Manager. 

Items defined in red are required values (note : global properties are supported). 

![Defining the Agent](../static/img/agent.png)

1.  Open Solution Manager.
2.  From the Home page select **Library**
3.  From the ***Administration*** Menu select **Agents**.
4.  Select **+Add** to add a new agent definition.
5.  Fill in the agent details
    - Insert a unique name for the connection.
    - Select **Kubernetes Job** from the **Type** drop-down list.
    - Select **General Settings**
    - Check that the NetCom Name is set to **Default** or the SMA Relay name if Relay is being used. 
    - Select **Kubernetes Job Settings**
   - In the **Config Script** section select the script containing the .kube/config information.
    - In the **Retain Log files** field enter the vault indicating how long log files should be retained.  
6.  Save the definition changes. 
7.  Start the connection by selecting the **Change Communication Status** button and selecting **Enable Full Comm.**. 

