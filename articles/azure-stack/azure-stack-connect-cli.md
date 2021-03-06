---
title: Connect to Azure Stack with CLI | Microsoft Docs
description: Learn how to use the cross-platform command-line interface (CLI) to manage and deploy resources on Azure Stack
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''

ms.assetid: f576079c-5384-4c23-b5a4-9ae165d1e3c3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: helaw

---
# Install and configure Azure Stack CLI
In this document, we guide you through the process of using Azure Command-line Interface (CLI) to manage Azure Stack resources on Linux and Mac client platforms.

## Install Node.js and npm
As a prerequisite, install version 4.6.2 of Node.js. On Linux, installation can be done with the following command:

```
wget -qO- https://deb.nodesource.com/setup_4.x | sudo bash -
sudo apt-get install nodejs
```

## Install Azure Stack CLI
If you’re on Mac or Linux, you can get the CLI by using the following command:

```
npm install -g azure-cli@0.10.4
```


## Connect to Azure Stack
In the following steps, you configure Azure CLI to connect to Azure Stack. Then you sign in and retrieve subscription information.

1. Retrieve the value for active-directory-resource-id by executing this PowerShell:
    ```PowerShell
    (Invoke-RestMethod -Uri https://api.local.azurestack.global/metadata/endpoints?api-version=1.0 -Method Get).authentication.audiences[0]
    ```
2. Use the following CLI command to add the Azure Stack environment, making sure to update *--active-directory-resource-id* with the data URL retrieved in the previous step:
   
          azure account env add AzureStack --resource-manager-endpoint-url "https://api.local.azurestack.global" --management-endpoint-url "https://api.local.azurestack.global" --active-directory-endpoint-url  "https://login.windows.net" --portal-url "https://publicportal.local.azurestack.global" --gallery-endpoint-url "https://publicportal.local.azurestack.global" --active-directory-resource-id "https://local.azurestack.global-api/" --active-directory-graph-resource-id "https://graph.windows.net/"
3. Sign in by using the following command (replace *username* with your user name):
   
       azure login -e AzureStack -u “<username>”
   
   > [!NOTE]
   > If you're getting certificate validation issues, disable certificate validation by running the command `set         NODE_TLS_REJECT_UNAUTHORIZED=0`.
   > 
   > 
4. Set the Azure configuration mode to Azure Resource Manager by using the following command:
   
       azure config mode arm
5. Retrieve a list of subscriptions.
   
       azure account list     

## Next steps
[Deploy templates with Azure CLI](azure-stack-deploy-template-command-line.md)

[Connect with PowerShell](azure-stack-connect-powershell.md)

[Manage user permissions](azure-stack-manage-permissions.md)

