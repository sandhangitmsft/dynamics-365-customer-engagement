---
title: "Export a solution for a specific Dynamics 365 version (Developer Guide for Dynamics 365 Customer Engagement)| MicrosoftDocs"
description: "Learn how to target and manage which Dynamics 365 version you wish to export a solution for"
ms.custom: ""
ms.date: 10/31/2017
ms.reviewer: ""
ms.service: "crm-online"
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "Dynamics 365 (online)"
ms.assetid: d4b9fe60-1d33-4588-abae-192ead9c1d22
caps.latest.revision: 23
author: "JimDaly"
ms.author: "jdaly"
manager: "amyla"
---
# Export a solution for a specific Dynamics 365 version

[!INCLUDE[](../includes/cc_applies_to_update_9_0_0.md)]

> [!NOTE]
>  This topic describes functionality that is available for minor version updates to major versions of [!INCLUDE[pn_dynamics_crm](../includes/pn-dynamics-crm.md)] Customer Engagement. This capability is not available for the initial release of [!INCLUDE[pn_dynamics_crm_online](../includes/pn-dynamics-crm-online.md)], but will be when minor version updates included additional functionality.  

 Each new version of [!INCLUDE[pn_dynamics_crm](../includes/pn-dynamics-crm.md)] will contain capabilities not found in earlier versions. Solutions that use new capabilities can’t be imported into an earlier version organization. Solutions exported from older version organizations can be imported into newer version organizations.  

 After you upgrade the organization you use to define your solution, you can still export a solution that targets an earlier version. When you select a lower target version any solution components that depend on capabilities introduced since that version won’t be included in the solution you export.  

> [!NOTE]
>  You can’t select an earlier version when you export the default solution.  

<a name="BKMK_ExportSolutionForVersion"></a>   
## Target a specific version when you export a solution  
 When you export a solution from [!INCLUDE[pn_crm_online_2015_update_1](../includes/pn-crm-online-2015-update-1.md)] you will have the option to target the solution for a specific Dynamics 365 version. For [!INCLUDE[pn_crm_online_2015_update_1](../includes/pn-crm-online-2015-update-1.md)] the options are 7.1 (default) and 7.0. When you choose 7.0, any new capabilities introduced in [!INCLUDE[pn_crm_online_2015_update_1](../includes/pn-crm-online-2015-update-1.md)] will not be included in the exported solution and any organizations still using earlier versions of [!INCLUDE[pn_crm_2015_shortest](../includes/pn-crm-2015-shortest.md)] will be able to install the solution.  

 When you export your solution to target an earlier version the export dialog can display two possible messages:  

 **This solution supports the target Dynamics 365 version**  
 This means that the solution components in your solution don’t depend on any capabilities or solution components introduced since that version.  

 **The following components are removed or modified as part of the export**  
 Below this message a table lists the solution component items that were modified or not included in the exported solution.  

 The information visible in the dialog can also be found in the exported solution file. When you export a solution to target a specific version, the name of the file will specify the target solution using the following naming convention:*Solution Name*<em>*Solution_Version_Number*_target_CRM\\</em>*Target Dynamics 365 version number*.zip. For example, an unmanaged solution with the name Sample Solution with solution version 2.0 that is exported to target the version 7.0 will have the name SampleSolution_2_0_target_CRM_7.0.zip. When you extract the contents of this compressed file you will find a filteredcomponents.xml file containing data detailing which actions were performed. You can open this file using Excel to view a report of which solution components were edited or removed.  

<a name="BKMK_Changes"></a>   
## What changes are applied to a solution exported for an earlier version?  
 Starting with the [!INCLUDE[pn_crm_2013_shortest](../includes/pn-crm-2013-shortest.md)] and [!INCLUDE[pn_crm_online_fall13](../includes/pn-crm-online-fall13.md)] releases, each type of solution component has an `IntroducedVersion` property. This value captures the current version number of the solution that the solution component was associated with when it was created. All solution components introduced by Microsoft are part of a hidden system solution where the version number corresponds with the [!INCLUDE[pn_dynamics_crm](../includes/pn-dynamics-crm.md)] version.  


| IntroducedVersion Value |                                                             Solution components introduced                                                             |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|         5.0.0.0         | Before [!INCLUDE[pn_crm_2013_shortest](../includes/pn-crm-2013-shortest.md)] and [!INCLUDE[pn_crm_online_fall13](../includes/pn-crm-online-fall13.md)] |
|         6.0.0.0         |    [!INCLUDE[pn_crm_2013_shortest](../includes/pn-crm-2013-shortest.md)] and [!INCLUDE[pn_crm_online_fall13](../includes/pn-crm-online-fall13.md)]     |
|         6.1.0.0         |     [!INCLUDE[pn_crm_2013_sp](../includes/pn-crm-2013-sp.md)] and [!INCLUDE[pn_v6_online_ur1_shortest](../includes/pn-v6-online-ur1-shortest.md)]      |
|         7.0.0.0         |                                  [!INCLUDE[pn_crm_2015_and_online_full](../includes/pn-crm-2015-and-online-full.md)]                                   |
|         7.1.0.0         |                                  [!INCLUDE[pn_crm_online_2015_update_1](../includes/pn-crm-online-2015-update-1.md)]                                   |
|         8.0.0.0         |               [!INCLUDE[pn_crm_online_2016_update_shortest](../includes/pn-crm-online-2016-update-shortest.md)] and CRM 2016 on-premises               |
|         8.1.0.0         |          [!INCLUDE[pn_crm_8_1_0_online](../includes/pn-crm-8-1-0-online.md)] and [!INCLUDE[pn_crm_8_1_0_op](../includes/pn-crm-8-1-0-op.md)]           |
|         8.2.0.0         |                                            [!INCLUDE[pn_crm_8_2_0_both](../includes/pn-crm-8-2-0-both.md)]                                             |
|         9.0.0.0         |                                          [!INCLUDE[pn_crm_9_0_0_online](../includes/pn-crm-9-0-0-online.md)]                                           |

 The `IntroducedVersion` data is used when exporting the solution to match the target version. This can result in three possible actions:  

 **Remove**  
 Solution components that did not exist in the target version or contains dependencies on components that can’t work with the target version won’t be added to the solution.  

 **Modify**  
 When a solution component has a dependency on a solution component that is removed, when possible, the solution component will be modified to remove the dependency. For example, if a form definition references an attribute that did not exist in that version; the form will be modified to remove that reference. If the solution component cannot be modified to remove the dependency the solution component will be removed.  

 **Replace**  
 When a solution component existed in the targeted version but was modified to have a dependency on a solution component that will be removed, that solution component may be replaced with the definition of the solution component that was defined for the targeted version.  

<a name="BKMK_TargetVersion"></a>   
## Select a target version programmatically  
 Use the <xref:Microsoft.Crm.Sdk.Messages.ExportSolutionRequest> to export a solution programmatically. After [!INCLUDE[pn_crm_2013_shortest](../includes/pn-crm-2013-shortest.md)] and [!INCLUDE[pn_crm_online_fall13](../includes/pn-crm-online-fall13.md)] this message has a new optional <xref:Microsoft.Crm.Sdk.Messages.ExportSolutionRequest.TargetVersion>`String` property you can use to set to “7.0.0.0” if you wish to export to the earlier version.  

### See also  
 [Package and distribute extensions using solutions](package-distribute-extensions-use-solutions.md)   
 [Create, Export, or Import an Unmanaged Solution](create-export-import-unmanaged-solution.md)   
 [Create, Install, and Update a Managed Solution](create-install-update-managed-solution.md)   
 [Maintain Managed Solutions](maintain-managed-solutions.md)   
 [Customization Guide: Use solutions for your customizations](http://go.microsoft.com/fwlink/p/?LinkID=322003)
