---
title: "Add teamsAppDefinition"
description: "Add teamsAppDefinition by posting to the teamsAppDefinition collection."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Add teamsAppDefinition
Namespace: microsoft.graph

Add teamsAppDefinition by posting to the teamsAppDefinition collection.

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
POST /chats/{chatsId}/installedApps/{teamsAppInstallationId}/teamsApp/appDefinitions/$ref
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [teamsAppDefinition](../resources/teamsappdefinition.md) object.

The following table shows the properties that are required when you create the [teamsAppDefinition](../resources/teamsappdefinition.md).

|Property|Type|Description|
|:---|:---|:---|
|id|String|**TODO: Add Description**|
|teamsAppId|String|**TODO: Add Description**|
|azureADAppId|String|**TODO: Add Description**|
|displayName|String|**TODO: Add Description**|
|version|String|**TODO: Add Description**|
|requiredResourceSpecificApplicationPermissions|String collection|**TODO: Add Description**|
|publishingState|teamsAppPublishingState|**TODO: Add Description**. Possible values are: `submitted`, `rejected`, `published`, `unknownFutureValue`.|
|shortdescription|String|**TODO: Add Description**|
|description|String|**TODO: Add Description**|
|lastModifiedDateTime|DateTimeOffset|**TODO: Add Description**|
|createdBy|[identitySet](../resources/identityset.md)|**TODO: Add Description**|



## Response

If successful, this method returns a `204 No Content` response code and a [teamsAppDefinition](../resources/teamsappdefinition.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "create_teamsappdefinition_from_"
}
-->
``` http
POST https://graph.microsoft.com/beta/chats/{chatsId}/installedApps/{teamsAppInstallationId}/teamsApp/appDefinitions/$ref
Content-Type: application/json
Content-length: 419

{
  "@odata.type": "#Microsoft.Teams.GraphSvc.teamsAppDefinition",
  "teamsAppId": "String",
  "azureADAppId": "String",
  "displayName": "String",
  "version": "String",
  "requiredResourceSpecificApplicationPermissions": [
    "String"
  ],
  "publishingState": "String",
  "shortdescription": "String",
  "description": "String",
  "createdBy": {
    "@odata.type": "microsoft.graph.identitySet"
  }
}
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "Microsoft.Teams.GraphSvc.teamsAppDefinition"
}
-->
``` http
HTTP/1.1 204 No Content

Content-Type: application/json
{
  "@odata.type": "#Microsoft.Teams.GraphSvc.teamsAppDefinition",
  "id": "1cb2abe6-abe6-1cb2-e6ab-b21ce6abb21c",
  "teamsAppId": "String",
  "azureADAppId": "String",
  "displayName": "String",
  "version": "String",
  "requiredResourceSpecificApplicationPermissions": [
    "String"
  ],
  "publishingState": "String",
  "shortdescription": "String",
  "description": "String",
  "lastModifiedDateTime": "String (timestamp)",
  "createdBy": {
    "@odata.type": "microsoft.graph.identitySet"
  }
}
```

