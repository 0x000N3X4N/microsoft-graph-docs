---
title: "Create macOSSoftwareUpdateConfiguration"
description: "Create a new macOSSoftwareUpdateConfiguration object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Create macOSSoftwareUpdateConfiguration
Namespace: microsoft.graph

Create a new [macOSSoftwareUpdateConfiguration](../resources/macossoftwareupdateconfiguration.md) object.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from most to least privileged)|
|:---|:---|
|Delegated (work or school account)|**TODO: Provide applicable permissions.**|
|Delegated (personal Microsoft account)|**TODO: Provide applicable permissions.**|
|Application|**TODO: Provide applicable permissions.**|

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
POST ** Collection URI for microsoft.graph.macOSSoftwareUpdateConfiguration not found
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [macOSSoftwareUpdateConfiguration](../resources/macossoftwareupdateconfiguration.md) object.

The following table shows the properties that are required when you create the [macOSSoftwareUpdateConfiguration](../resources/macossoftwareupdateconfiguration.md).

|Property|Type|Description|
|:---|:---|:---|
|id|String|**TODO: Add Description** Inherited from [entity](../resources/entity.md)|
|lastModifiedDateTime|DateTimeOffset|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|roleScopeTagIds|String collection|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|supportsScopeTags|Boolean|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|deviceManagementApplicabilityRuleOsEdition|[deviceManagementApplicabilityRuleOsEdition](../resources/intune-devicemanagementapplicabilityruleosedition.md)|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|deviceManagementApplicabilityRuleOsVersion|[deviceManagementApplicabilityRuleOsVersion](../resources/intune-devicemanagementapplicabilityruleosversion.md)|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|deviceManagementApplicabilityRuleDeviceMode|[deviceManagementApplicabilityRuleDeviceMode](../resources/intune-devicemanagementapplicabilityruledevicemode.md)|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|createdDateTime|DateTimeOffset|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|description|String|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|displayName|String|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|version|Int32|**TODO: Add Description** Inherited from [deviceConfiguration](../resources/intune-deviceconfiguration.md)|
|criticalUpdateBehavior|macOSSoftwareUpdateBehavior|**TODO: Add Description**. Possible values are: `notConfigured`, `default`.|
|configDataUpdateBehavior|macOSSoftwareUpdateBehavior|**TODO: Add Description**. Possible values are: `notConfigured`, `default`.|
|firmwareUpdateBehavior|macOSSoftwareUpdateBehavior|**TODO: Add Description**. Possible values are: `notConfigured`, `default`.|
|allOtherUpdateBehavior|macOSSoftwareUpdateBehavior|**TODO: Add Description**. Possible values are: `notConfigured`, `default`.|
|updateScheduleType|macOSSoftwareUpdateScheduleType|**TODO: Add Description**. Possible values are: `alwaysUpdate`, `updateDuringTimeWindows`, `updateOutsideOfTimeWindows`.|
|customUpdateTimeWindows|[customUpdateTimeWindow](../resources/intune-customupdatetimewindow.md) collection|**TODO: Add Description**|
|updateTimeWindowUtcOffsetInMinutes|Int32|**TODO: Add Description**|



## Response

If successful, this method returns a `201 Created` response code and a [macOSSoftwareUpdateConfiguration](../resources/macossoftwareupdateconfiguration.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "create_macossoftwareupdateconfiguration_from_"
}
-->
``` http
POST https://graph.microsoft.com/beta** Collection URI for microsoft.graph.macOSSoftwareUpdateConfiguration not found
Content-Type: application/json
Content-length: 1010

{
  "@odata.type": "#microsoft.graph.macOSSoftwareUpdateConfiguration",
  "roleScopeTagIds": [
    "String"
  ],
  "supportsScopeTags": "Boolean",
  "deviceManagementApplicabilityRuleOsEdition": {
    "@odata.type": "microsoft.graph.deviceManagementApplicabilityRuleOsEdition"
  },
  "deviceManagementApplicabilityRuleOsVersion": {
    "@odata.type": "microsoft.graph.deviceManagementApplicabilityRuleOsVersion"
  },
  "deviceManagementApplicabilityRuleDeviceMode": {
    "@odata.type": "microsoft.graph.deviceManagementApplicabilityRuleDeviceMode"
  },
  "description": "String",
  "displayName": "String",
  "version": "Integer",
  "criticalUpdateBehavior": "String",
  "configDataUpdateBehavior": "String",
  "firmwareUpdateBehavior": "String",
  "allOtherUpdateBehavior": "String",
  "updateScheduleType": "String",
  "customUpdateTimeWindows": [
    {
      "@odata.type": "microsoft.graph.customUpdateTimeWindow"
    }
  ],
  "updateTimeWindowUtcOffsetInMinutes": "Integer"
}
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.macOSSoftwareUpdateConfiguration"
}
-->
``` http
HTTP/1.1 201 Created

Content-Type: application/json
{
  "@odata.type": "#microsoft.graph.macOSSoftwareUpdateConfiguration",
  "id": "0aaaf334-f334-0aaa-34f3-aa0a34f3aa0a",
  "lastModifiedDateTime": "String (timestamp)",
  "roleScopeTagIds": [
    "String"
  ],
  "supportsScopeTags": "Boolean",
  "deviceManagementApplicabilityRuleOsEdition": {
    "@odata.type": "microsoft.graph.deviceManagementApplicabilityRuleOsEdition"
  },
  "deviceManagementApplicabilityRuleOsVersion": {
    "@odata.type": "microsoft.graph.deviceManagementApplicabilityRuleOsVersion"
  },
  "deviceManagementApplicabilityRuleDeviceMode": {
    "@odata.type": "microsoft.graph.deviceManagementApplicabilityRuleDeviceMode"
  },
  "createdDateTime": "String (timestamp)",
  "description": "String",
  "displayName": "String",
  "version": "Integer",
  "criticalUpdateBehavior": "String",
  "configDataUpdateBehavior": "String",
  "firmwareUpdateBehavior": "String",
  "allOtherUpdateBehavior": "String",
  "updateScheduleType": "String",
  "customUpdateTimeWindows": [
    {
      "@odata.type": "microsoft.graph.customUpdateTimeWindow"
    }
  ],
  "updateTimeWindowUtcOffsetInMinutes": "Integer"
}
```

