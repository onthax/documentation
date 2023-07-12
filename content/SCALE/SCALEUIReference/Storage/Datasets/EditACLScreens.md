---
title: "Edit ACL Screens"
description: "Describes the ACL permissions screens, settings for POSIX and NFSv4 ACLs, and the conditions that result in additional setting options."
weight: 55
aliases: 
tags:
 - scaleacls
 - scaledatasets
 - scalestorage
---

{{< toc >}}

TrueNAS SCALE offers two ACL types: POSIX (the SCALE default) and NFSv4. 
For a more in-depth explanation of ACLs and configurations in TrueNAS SCALE, see our [ACL Primer]({{< relref "ACLPrimer.md" >}}).

The **ACL Type** setting, found in the **Advanced Options** of both the **Add Dataset** and **Edit Dataset** screens, determines the ACL presets available on the **Select a preset ACL** window and also determines which permissions editor screens you see after you click the <span class="material-icons">edit</span> edit icon on the **Dataset Permissions** widget.

If **ACL Type** is set to **NSFv4**, you can select the **ACL Mode** you want to use. 

{{< hint type=tip >}}
NFSv4 is an access control list (ACL) type not related to the share type you might use (SMB or NFS).
{{< /hint >}}

## Unix Permissions Editor Screen

If you selected **POSIX** or **Inherit** as your ACL type, the first screen you see after you click edit on the **Dataset Permissions** widget is the **Storage > Edit Permissions** screen with the **Unix Permissions Editor** basic ACL configuration settings.

![EditPermissionsUnixPermissionsEditor](/images/SCALE/22.12/EditPermissionsUnixPermissionsEditor.png "Edit Permissions Unix Permissions Editor")

Use the settings on this screen to configure basic ACL permissions.

### Owner Settings

The **Owner** section controls which TrueNAS user and group has full control of this dataset.

{{< expand "Click here for details" "v" >}}
{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **User** | Enter or select a user to control the dataset. Users created manually or imported from a directory service appear in the menu. |
| **Apply User** | Select to confirm user changes. To prevent errors, TrueNAS only submits changes only after you select this option. |
| **Group** | Enter or select the group to control the dataset. Groups created manually or imported from a directory service appear in the menu. |
| **Apply Group** | Select to confirm group changes. To prevent errors, TrueNAS only submits changes only after you select this option. |
{{< /truetable >}}
{{< /expand >}}

### Access Settings
The **Access** section lets users define the basic **Read**, **Write**, and **Execute** permissions for the **User**, **Group**, and **Other** accounts that might access this dataset.

{{< hint type=important >}}
A common misconfiguration is removing the **Execute** permission from a dataset that is a parent to other child datasets.
Removing this permission results in lost access to the path.
{{< /hint >}}

### Advanced Settings

The **Advanced** section lets users **Apply Permissions Recursively** to all directories, files, and child datasets within the current dataset. 

To access advanced POSIX ACL settings, click **Add ACL** on the **Unix Permissions Editor**. The **Select a preset ACL** window displays with two radio buttons. 

## Select A Preset ACL

{{< hint type=important >}}
Selecting a preset replaces the ACL currently displayed on the Edit ACL screen and deletes any unsaved changes.
{{< /hint >}}

There are two different **Select a preset ACL** windows. 

{{< expand "Click here for details" "v" >}}
If using **POSIX** or **Inherit** as the **ACL Type** setting, the window with three setting options displays before you see the **Edit ACL** screen. 
These setting options allow you to select and use a pre-configured set of permissions that match general permissions situations or to create a custom set of permissions. 
You can add to a pre-configured ACL preset on the **Edit ACL** screen.

![PosixSelectAPresetACLWindow](/images/SCALE/22.12/PosixSelectAPresetACLWindow.png "POSIX Select a Preset ACL")

If using **NFSv4** as the **ACL Type** setting, you access the NFS4 **Select a Preset ACL** window from the **Edit ACL** screen by clicking **Use Preset ACL**.

![NFS4SelectAPresetACLDialog](/images/SCALE/22.12/NFS4SelectAPresetACLWindow.png "NFS4 Select a Preset ACL")

The **ACL Type** setting determines the pre-configured options presented on the **Default ACL Options** dropdown list on each of these windows. 
For POSIX, the options are **POSIX_OPEN**, **POSIX_RESTRICTED**, or **POSIX_HOME**. For NFSv4, the options are **NFS4_OPEN**, **NFS4_RESTRICTED**, **NFS4_HOME**, and **NFS4_DOMAIN_HOME**.

{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **Select a preset ACL** | Click this radio button to populate the **Default ACL Options** dropdown list with a set of pre-configured POSIX permissions. |
| **Create a custom ACL** | Click this radio button to display the **Edit ACL** screen with no default permissions, users, or groups to configure your own set of permissions after you click **Continue**. |
{{< /truetable >}}

Click **Continue** to display the **Edit ACL** screen.
{{< /expand >}}

## Edit ACL Screen

The **Edit ACL** screen displays different options based on the **ACL Type** setting on the **Add Dataset** or **Edit Dataset** screen in the **Advanced Options** section.

The section below describes the differences between screens for each ACL type.

### ACL Editor Settings - POSIX and NFSv4

Select any user account or group manually entered or imported from a directory service in the **Owner** or **Owner Group**. The value entered or selected in each field displays in the **Access Control List** below these fields. 

**Dataset** displays the dataset path (name) you selected to edit.

![ACLEditorSettings](/images/SCALE/23.10/ACLEditorSettings.png "ACL Editor Settings") 

### Access Control List - POSIX and NFS4

The **Access Control List** section displays the items and a permissions summary for the **owner@**, **group@**, and **everyone@** for both POSIX and NSFv4 ACL types. The list of items changes based on a selected pre-configured set of permissions.

To add a new item to the ACL, click **Add Item**, define **Who** the Access Control Entry (ACE) applies to, and configure permissions and inheritance flags for the ACE.

### Edit ACL Functions - POSIX and NFS4

These functions display on the **Edit ACL** screen for both POSIX and NSFv4 ACL types except for **Strip ACL**, which only displays for NSFv4 types.

{{< expand "Click here for details" "v" >}}
![EditACLScreenNFSv4Type](/images/SCALE/22.12/EditACLScreenNFSv4Type.png "NFS4 Edit ACL Screen") 

{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **Add Item** | Adds a new ACE to the **Access Control List**. |
| **Apply permissions recursively** | Select to apply all settings or changes on the **Edit ACL** screen to all child datasets in the path in **Dataset**. |
| **Save Access Control List** | Saves settings or changes made on the **Edit ACL** screen. |
| **Strip ACL** | (NSFv4 only) Remove all ACLs from the current dataset and any directories or files contained within this dataset. Stripping the ACL resets dataset permissions and can make data inaccessible until you create new permissions. |
| **Permissions Editor** | (POSIX only) Displays the **Unix Permissions Editor** screen for POSIX ACL types. |
| **Use Preset** | Displays the **Select a preset ACL** window. If the **ACL Type** setting, found in the **Advanced Options** of both the **Add Dataset** and **Edit Dataset** screens, is **POSIX** or **Inherit**, the **Default ACL Options** dropdown displays POSIX pre-configured options. If set to NFSv4, the preset options displayed are pre-configured NSFv4 options. |
| **Save As Preset** | Saves the current access control list as a custom preset and adds it to the **Access Control List**. |
{{< /truetable >}}

{{< /expand >}}

### POSIX Access Control Entry Settings
The POSIX **Access Control Entry** settings include **Who**, **Permissions**, and **Flags** options.

{{< expand "Click here for details" "v" >}}
![EditACLPOSIXAccessControlEntrySettings](/images/SCALE/22.12/EditACLPOSIXAccessControlEntrySettings.png "POSIX Access Control Entry Settings")

{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **Who** | Select the user or group from the dropdown list the permissions apply to. <br><br>**User** denotes access rights for users identified by the entry qualifier.<br>**Group** denotes access rights for the filegroup.<br>**Other** denotes access rights for processes that do not match any other entry in the ACL.<br>**Group Obj** denotes access rights for the filegroup.<br>**User Obj** denotes access rights for the file owner.<br>**Mask** denotes the maximum access rights User, Group Obj, or Group type entries can grant. |
| **Permissions** | Select the checkbox for each permission type (**Read**, **Write** and **Execute**) to apply to the user or group in **Who**.
| **Flags** | Select the **Default** option to include a flag setting for the user or group in **Who**. |
{{< /truetable >}}

{{< /expand >}}

### NFS4 Access Control Entry Settings

There are two **Access Control Entry** settings, **Who** and **ACL Type**. 

{{< expand "Click here for details" "v" >}}
The NFSv4 **ACL Type** radio buttons change the **Permissions** and **Flags** setting options. Select **Allow** to grant the specified permissions or **Deny** to restrict the permissions for the user or group in **Who**. 

![EditACLNFSv4AccessControlEntrySettings](/images/SCALE/22.12/EditACLNFSv4AccessControlEntrySettings.png "NSFv4 Access Control Entry Settings")

{{< truetable >}}
| Setting | Description |
|---------|-------------|
| **Who** | Access Control Entry (ACE) user or group. Select a specific User or Group for this entry. See [nfs4_setfacl(1) NFSv4 ACL ENTRIES](https://man7.org/linux/man-pages/man1/nfs4_setfacl.1.html). <br><br>**User** denotes access rights for users identified by the qualifier.<br>**Group** denotes access rights for groups identified by the qualifier.<br>**owner@** applies this entry to the user that owns the dataset.<br>**group@** applies this entry to the group that owns the dataset. <br>**everyone@** applies this entry to all users and groups. |
| **ACL Type** | Determines how the Permissions apply to the chosen **Who**. Choose **Allow** to grant the specified permissions and **Deny** to restrict the specified permissions. |
{{< /truetable >}}

{{< /expand >}}

### NFS4 Permissions and Flags

TrueNAS divides permissions and inheritance flags into basic and advanced options. The basic permissions options are commonly-used groups of advanced options.
Basic inheritance flags only enable or disable ACE inheritance. Advanced flags offer finer control for applying an ACE to new files or directories.

#### Permissions Settings - Basic

Click the **Basic** radio button to display the **Permissions** dropdown list of options that applies to the user or group in **Who**.

{{< expand "Click here for details" "v" >}}
![EditACLNFSv4BasicPermissionsOptions](/images/SCALE/22.12/EditACLNFSv4BasicPermissionsOptions.png "NSFv4 Basic Permissions Options") 

{{< truetable >}}
| Permission | CLI Command | Description |
|------------|-------------|-------------|
| **Read** | `r-x---a-R-c---` | View file or directory contents, attributes, named attributes, and ACL. | 
| **Modify** | `rwxpDdaARWc--s` | Adjust file or directory contents, attributes, and named attributes. Create new files or subdirectories. Includes the *Traverse* permission. | 
| **Traverse** | `--x---a-R-c---` | Execute a file or move through a directory. | 
| **Full Control** | `rwxpDdaARWcCos` | Apply all permissions. | 
{{< /truetable >}}
{{< /expand >}}

#### Permissions Settings - Advanced

Click the **Advanced** radio button to display the **Permissions** options for the user or group in **Who**.

{{< expand "Click here for details" "v" >}}
![EditACLNSFv4AdvancedPermissionsOptions](/images/SCALE/22.12/EditACLNSFv4AdvancedPermissionsOptions.png "NSFv4 Advanced Permissions Options") 

{{< truetable >}}
| Permission | CLI Command | Description |
|------------|-------------|-------------|
| **Read Data** | `r` | View file contents or list directory contents. | 
| **Write Data** | `w` | Create new files or modify any part of a file. | 
| **Append Data** | `p` | Add new data to the end of a file. | 
| **Read Named Attributes** | `R` | View the named attributes directory. | 
| **Write Named Attributes** | `W` | Create a named attribute directory. Must be paired with the Read Named Attributes permission. | 
| **Execute** | `x` | Execute a file, move through, or search a directory. | 
| **Delete Children** | `D` | Delete files or subdirectories from inside a directory. | 
| **Read Attributes** | `a` | View file or directory non-ACL attributes. | 
| **Write Attributes** | `A` | Change file or directory non-ACL attributes. | 
| **Delete** | `d` | Remove the file or directory. | 
| **Read ACL** | `c` | View the ACL. | 
| **Write ACL** | `C` | Change the ACL and the ACL mode. | 
| **Write Owner** | `o` | Change the user and group owners of the file or directory. | 
| **Synchronize** | `s` | Synchronous file read/write with the server. This permission does not apply to FreeBSD clients. |
{{< /truetable >}}
{{< /expand >}}

#### Flag Settings - Basic

Click the **Basic** radio button to display the flag settings that enable or disable ACE inheritance.

{{< expand "Click here for details" "v" >}}
![EditACLNSFv4BasicFlagsOptions](/images/SCALE/22.12/EditACLNSFv4BasicFlagsOptions.png "NSFv4 Basic Flags Options")

{{< truetable >}}
| Flag | CLI Command | Description |
|------|-------------|-------------|
| **Inherit** | `fd-----` | Enable ACE inheritance. | 
| **No Inherit** | `-------` | Disable ACE inheritance. | 
{{< /truetable >}}

{{< /expand >}}

#### Flag Settings - Advanced

Click the **Advanced** radio button to display the flag settings that enable or disable ACE inheritance and offer finer control for applying an ACE to new files or directories.

{{< expand "Click here for details" "v" >}}
![EditACLNSFv4AdvancedFlagsOptionst](/images/SCALE/22.12/EditACLNSFv4AdvancedFlagsOptions.png "NFSv4 Advanced Flags Options") 

{{< truetable >}}
| Flag | CLI Command | Description |
|------|-------------|-------------|
| **File Inherit** | `f` | The ACE is inherited with subdirectories and files. It applies to new files. | 
| **Directory Inherit** | `d` | New subdirectories inherit the full ACE. | 
| **No Propagate Inherit** | `n` | The ACE can only be inherited once. | 
| **Inherit Only** | `i` | Remove the ACE from permission checks but allow new files or subdirectories to inherit it. Inherit Only is removed from these new objects. | 
| **Inherited** | `I` | Set when this dataset inherits the ACE from another dataset. |
{{< /truetable >}}
{{< /expand >}}


{{< taglist tag="scaleacls" limit="10" >}}
{{< taglist tag="scaledatasets" limit="10" title="Related Dataset Articles" >}}