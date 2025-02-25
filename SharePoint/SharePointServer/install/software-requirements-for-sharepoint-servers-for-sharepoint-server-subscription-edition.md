---
title: "Software requirements for SharePoint Servers for SharePoint Server Subscription Edition"
ms.reviewer: 
ms.author: serdars
author: nimishasatapathy
manager: serdars
ms.date: 03/14/2023
audience: ITPro
f1.keywords:
- NOCSH
ms.topic: conceptual
ms.service: sharepoint-server-itpro
ms.localizationpriority: medium
ms.collection:
- IT_Sharepoint_Server
- IT_Sharepoint_Server_Top
ms.assetid: 
description: "This article describes the software requirements for SharePoint Server."
---

# Software requirements for SharePoint Servers for SharePoint Server Subscription Edition

[!INCLUDE [appliesto-xxx-xxx-xxx-SUB-xxx-md](../includes/appliesto-xxx-xxx-xxx-SUB-xxx-md.md)] 

## Operating systems

SharePoint Server supports the following operating systems:

- [Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) Standard or Datacenter
- [Windows Server 2022](https://www.microsoft.com/evalcenter/evaluate-windows-server-2022) Standard or Datacenter
- [Windows Server 2025](https://www.microsoft.com/evalcenter/evaluate-windows-server-2025) Standard or Datacenter

SharePoint Server Subscription Edition supports the following Windows Server installation options:

- Server with Desktop Experience
- Server Core

> [!NOTE]
> Microsoft doesn't support installing Microsoft Office and SharePoint Server Subscription Edition on the same computer.

> [!NOTE]
> The minimum Microsoft Office version supported with SharePoint Server Subscription Edition is Microsoft Office 2013.

## Prerequisites 

SharePoint Server Subscription Edition requires additional software prerequisites. Those prerequisites can be installed through the `prerequisiteinstaller.exe` tool on the SharePoint Server Subscription Edition installation disc, or manually as described below.

### Software prerequisites

The SharePoint Server Subscription Edition prerequisite installer (`prerequisiteinstaller.exe`) installs the following softwares in the order as listed if they haven't already been installed on the target server:

1. Web Server (IIS) Role

2. [Microsoft .NET Framework 4.8](https://go.microsoft.com/fwlink/?LinkId=2085155)

3. [Visual C++ Redistributable Package for Visual Studio 2015-2019](https://go.microsoft.com/fwlink/?LinkId=2130438)

    > [!NOTE]
    > SharePoint Server Subscription Edition will require the Visual C++ 2015-2022 Redistributable (x64) as a software prerequisite starting with SharePoint Server Subscription Edition Version 23H1. This new software prerequisite replaces the Visual C++ Redistributable Package for Visual Studio 2015-2019. This new software prerequisite won't be installed by the prerequisiteinstaller.exe tool but by the SharePoint Server Subscription Edition Version 23H1 feature update if it isn't already installed. For information on how to download and install it separately, see [Visual C++ 2015-2022 Redistributable (x64)](https://go.microsoft.com/fwlink/?LinkId=2224881).

### Prerequisite installer operation and command-line options

You can run `prerequisiteinstaller.exe` with no parameters or at a command prompt with the following optional parameters: 

- **/?**: This displays command-line options.

- **/continue**: This is used to tell the installer that it's continuing from a restart.

- **/unattended**: This indicates that the installer should run with no user interaction. This is typically used when scripting the installation.

When you run `prerequisiteinstaller.exe`, you might be asked to restart the server one or more times during the software installation process. If you're running it at a command prompt, you should continue the prerequisite installation by running `prerequisiteinstaller.exe` with the **/continue** parameter after restarting.

The prerequisite installer installs software from the file that you specify in the command-line options described in the following list:

- **/WindowsSource:<_path_>** Install any "Features on Demand (FOD)" Windows features from <_path_> instead of downloading them from Windows Update. Use this parameter if the computer doesn't have access to Windows Update. The <_path_> is typically the **\sources\sxs** folder on the Windows Server installation media.

  > [!NOTE]
  > **\<_path_\>** signifies the directory from which you want to install.

- **/DotNet48:<_file_>** Install Microsoft .NET Framework 4.8 from <_file_>.

  > [!NOTE]
  > **\<_file_\>** signifies the file from which you want to install.

- **/MSVCRT142:<_file_>** Install Visual C++ Redistributable Package for Visual Studio 2015-2019 from <_file_>.

  > [!IMPORTANT]
  > If you don't specify the **\<_file_\>** or **\<_path_\>** options, the installer downloads the file from the Internet and installs it. If the option doesn't apply to the current operating system, it's ignored.

The prerequisite installer creates log files at **%TEMP%\prerequisiteinstaller.\<date>.\<time>.log**. You can check these log files for specific details about all changes the installer makes to the target computer.

### Manually configure Windows Server Roles and Features

To manually configure the required Windows Server Roles and Features, you can use one of the following two methods:

1. Server Manager

2. Microsoft PowerShell

To configure by using Server Manager, see [Install or Uninstall Roles, Role Services, or Features](/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features).

To configure by using PowerShell, from a PowerShell command prompt window, type:

```PowerShell
Install-WindowsFeature NET-WCF-Pipe-Activation45,NET-WCF-HTTP-Activation45,NET-WCF-TCP-Activation45,Web-Server,Web-WebServer,Web-Common-Http,Web-Static-Content,Web-Default-Doc,Web-Dir-Browsing,Web-Http-Errors,Web-App-Dev,Web-Asp-Net45,Web-Net-Ext45,Web-ISAPI-Ext,Web-ISAPI-Filter,Web-Health,Web-Http-Logging,Web-Log-Libraries,Web-Request-Monitor,Web-Http-Tracing,Web-Security,Web-Basic-Auth,Web-Windows-Auth,Web-Filtering,Web-Performance,Web-Stat-Compression,Web-Dyn-Compression,WAS,WAS-Process-Model,WAS-Config-APIs -IncludeManagementTools
```

> [!NOTE]
> Some Windows features may be "Features on Demand (FOD)", which are downloaded from Windows Update.  If the computer doesn't have access to Windows Update, you can specify local installation files by adding the **Source** parameter to the `Install-WindowsFeature` PowerShell command and pointing to the **\sources\sxs** folder on the Windows Server installation media.
>
> For example: -Source D:\sources\sxs
