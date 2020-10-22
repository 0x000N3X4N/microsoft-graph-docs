---
title: "Get deviceManagementComplexSettingDefinition"
description: "Read the properties and relationships of a deviceManagementComplexSettingDefinition object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Get deviceManagementComplexSettingDefinition
Namespace: microsoft.graph

Read the properties and relationships of a [deviceManagementComplexSettingDefinition](../resources/intune-devicemanagementcomplexsettingdefinition.md) object.

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
GET /deviceManagementComplexSettingDefinition
```

## Optional query parameters
This method supports some of the OData query parameters to help customize the response. For general information, see [OData query parameters](/graph/query-parameters).

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|

## Request body
Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and a [deviceManagementComplexSettingDefinition](../resources/intune-devicemanagementcomplexsettingdefinition.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "get_devicemanagementcomplexsettingdefinition"
}
-->
``` http
GET https://graph.microsoft.com/beta/deviceManagementComplexSettingDefinition
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.deviceManagementComplexSettingDefinition"
}
-->
``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "value": {
    "@odata.type": "#microsoft.graph.deviceManagementComplexSettingDefinition",
    "id": "cc5da58c-a58c-cc5d-8ca5-5dcc8ca55dcc",
    "valueType": "String",
    "displayName": "String",
    "isTopLevel": "Boolean",
    "description": "String",
    "placeholderText": "String",
    "documentationUrl": "String",
    "headerTitle": "String",
    "headerSubtitle": "String",
    "keywords": [
      "String"
    ],
    "constraints": [
      {
        "@odata.type": "microsoft.graph.deviceManagementSettingAppConstraint"
      }
    ],
    "dependencies": [
      {
        "@odata.type": "microsoft.graph.deviceManagementSettingDependency"
      }
    ],
    "propertyDefinitionIds": [
      "String"
    ]
  }
}
```

