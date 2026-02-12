# KubernetesJob ACS Installation

Download the ACS KubernetsJob software from the SMA FTP Site.
Location will be in
**/OpCon Releases/Integrations/KUbernetesJob/** 
Select the required version.

- Unzip the KubernetesJob.zip file.
- On-prem customers 
  Copy the KubernetesJob directory to the \\SAM\\plugins directory
  Restart the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
- Cloud customers
  Copy the KubernetesJob directory to the \\Relay\\plugins directory
  Restart the **SMA OpCon Relay** service.

# KubernetesJob ACS Upgrade

Download the ACS KubernetesJob selected software upgrade from the SMA FTP Site.
Location will be in
**/OpCon Releases/Integrations/KubernetesJob/** 

- Unzip the KubernetesJob.zip file.
- On-prem customers 
  Stop the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
  Copy the KubernetesJob directory to the \\SAM\\plugins directory
  Restart the **SMA OpCon Services Manager** and **SMA OpCon RestAPI** service.
- Cloud customers
  Stop the **SMA OpCon Relay** service.
  Copy the KubernetesJob directory to the \\Relay\\plugins directory
  Restart the **SMA OpCon Relay** service.