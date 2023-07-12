---
title: "WG-Easy"
description: "Provides installation instructions for the WG-Easy application."
weight:
aliases:
 - /scale/scaletutorials/apps/installwgeasyapp/
tags:
- scaleopenvpn
---


{{< include file="content/_includes/SCALEServiceDeprecationNotice.md" type="page" >}}

This article provides installation instructions for the WG-Easy application. 
WG-Easy is a docker image designed to simplify setting up and managing WireGuard connections. 
WG-Easy provides a pre-configured environment that includes all the necessary components including a web-based user interface to manage VPN connections.

## Migrating from TrueNAS OpenVPN Services

If migrating from the SCALE OpenVPN client and server services to a new application for VPN servers, locate the VPN app you want to use on the Available Appliations screen.
If not listed, install the application using the **[Install Custom App]({{< relref "UsingCustomApp.md" >}})** screen. 

Before you configure a new VPN application:

* Disable OpenVPN services.
  Go to **System Settings > Services**, disable the services, and clear the **Start Automatically** checkboxes. 
  This prevents the services from re-enabling after a system restart.

* Review your client and server service settings. 
  Note all certificate, device type, port, protocol, TLS crypt authentication, and additional parameter settings. 

## Installing the WG-Easy Application 

To install the **wg-easy** application: 

Go to **Apps** click on **Available Applications** and locate the **wg-easy** application widget.

{{< trueimage src="/images/SCALE/22.12/WgeasyAppWidget.png" alt="WG-Easy Application Widget" id="1: WG-Easy Application Widget" >}}

Click **Install** to open the **wg-easy** configuration wizard.

{{< trueimage src="/images/SCALE/22.12/WgeasyApplicationName.png" alt="Install WG-Easy Application Name and Version" id="2: Install WG-Easy Application Name and Version" >}}

Accept the default value or enter a name in **Application Name**.

Enter the configuration settings. 
Enter the public host name or IP of your VPN server in **Hostname or IP**.

{{< trueimage src="/images/SCALE/22.12/WgeasyConfigSettings.png" alt="WG-Easy Configuration Settings" id="3: WG-Easy Configuration Settings" >}} 

If you use or want to protect access to the WG-Easy web UI, enter a password in **Password for WebUI**.

Accept the default values in **Persistent Keep Alive** and **Clients MTU** or enter the values you want to use. 
To change the time the connection remains alive, enter a value in seconds in **Persistent Keep Alive**. When set to zero, connections are not kept alive. 

Accept the default IPs in **Clients IP Address Range** and **Clients DNS Server** or enter the IP addresses the client uses.

To specify allowed IP addresses, click **Add** to the right of **Allowed IPs** for each IP address you want to enter. 
If you do not specify allowed IPs, the application uses 0.0.0.0/0.

{{< trueimage src="/images/SCALE/22.12/WgeasyConfigAddAllowIPAndEnvironments.png" alt="wg-easy Allowed IPs and Environments" id="4: wg-easy Allowed IPs and Environments" >}} 

To specify environment variables, click **Add** to the right of **WG-Easy Environment** for each environment variable you want to add. 
Variables you can add are listed in the table below.
{{< expand "Environment Variables" "v" >}}
{{< truetable >}}
| Variable | Description |
|----------|-------------|
| WD_DEVICE | Enter the interface name or ID for the ethernet device WireGuard traffic should forward through. |
| WG_PRE_UP | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
| WG_POST_UP | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
| WG_PRE_DOWN | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
| WG_POST_DOWN | See [config.js](https://github.com/WeeJeWel/wg-easy/blob/master/src/config.js#L19) for the default value. |
{{< /truetable >}}
{{< /expand >}}

Enter your storage settings. 
Select **Enable Custom Host Path for WG-Easy Configuration Volume** to add the **Host Path for WG-Easy Configuration Volume** field. 
Enter or browse to select the mount path for the host path.

{{< trueimage src="/images/SCALE/22.12/WgeasyStorageEnableCustomHostPath.png" alt="WG-Easy Add Custom Host Path" id="5: WG-Easy Add Custom Host Path" >}} 

To add additional host path volumes, click **Add** to the right of **Extra Host Path Volumes**. 

{{< trueimage src="/images/SCALE/22.12/WgeasyStorageAddExtraHostPathVolumes.png" alt="WG-Easy Add Extra Host Path Volumes" id="6: WG-Easy Add Extra Host Path Volumes" >}} 

Enter the path in **Mount Path in Pod** where you want to mount the volume inside the pod. 
Enter or browse to the host path for the WG-Easy application dataset.

Accept the default port numbers in **WireGuard UDP Node Port for WG-Easy** and **WebUI Node Port for WG-Easy**. 
WireGuard always listens on 51820 inside the Docker container. 
Refer to the TrueNAS [default port list]({{< relref "DefaultPorts.md" >}}) for a list of assigned port numbers.
To change the port numbers, enter a number within the range 9000-65535. 

{{< trueimage src="/images/SCALE/22.12/WgeasyNetworking.png" alt="WG-Easy Networking" id="7: WG-Easy Networking" >}} 

To add DNS configuration options, click **Add** to the right of **DNS Options**.

{{< trueimage src="/images/SCALE/22.12/WgeasyAddAdvancedDNS.png" alt="wg-easy Add DNS Options" id="8: wg-easy Add DNS Options" >}} 

Accept the default values in **Resources Configuration** or select **Enable Pod resource limits** to enter new CPU and memory values for the destination system.

{{< trueimage src="/images/SCALE/22.12/WgeasyEnableResourceLimits.png" alt="WG-Easy Enable Resource Limits" id="9: WG-Easy Enable Resource Limits" >}}

Click **Save**.

{{< taglist tag="scaleopenvpn" limit="10" >}}

