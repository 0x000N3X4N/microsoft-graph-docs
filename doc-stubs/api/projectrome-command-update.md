---
title: "Update command"
description: "Update the properties of a command object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Update command
Namespace: microsoft.graph

Update the properties of a [command](../resources/projectrome-command.md) object.

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
PATCH /commands/{commandsId}
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [command](../resources/projectrome-command.md) object.

The following table shows the properties that are required when you create the [command](../resources/projectrome-command.md).

|Property|Type|Description|
|:---|:---|:---|
|id|String|**TODO: Add Description** Inherited from [entity](../resources/entity.md)|
|status|String|**TODO: Add Description**|
|type|String|**TODO: Add Description**|
|appServiceName|String|**TODO: Add Description**|
|packageFamilyName|String|**TODO: Add Description**|
|error|String|**TODO: Add Description**|
|payload|[payloadRequest](../resources/projectrome-payloadrequest.md)|**TODO: Add Description**|
|permissionTicket|String|**TODO: Add Description**|
|postBackUri|String|**TODO: Add Description**|



## Response

If successful, this method returns a `200 OK` response code and an updated [command](../resources/projectrome-command.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "update_command"
}
-->
``` http
PATCH https://graph.microsoft.com/beta/commands/{commandsId}
Content-Type: application/json
Content-length: 316

{
  "@odata.type": "#microsoft.graph.command",
  "status": "String",
  "type": "String",
  "appServiceName": "String",
  "packageFamilyName": "String",
  "error": "String",
  "payload": {
    "@odata.type": "microsoft.graph.payloadRequest"
  },
  "permissionTicket": "String",
  "postBackUri": "String"
}
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true
}
-->
``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "@odata.type": "#microsoft.graph.command",
  "id": "a91196cc-96cc-a911-cc96-11a9cc9611a9",
  "status": "String",
  "type": "String",
  "appServiceName": "String",
  "packageFamilyName": "String",
  "error": "String",
  "payload": {
    "@odata.type": "microsoft.graph.payloadRequest"
  },
  "permissionTicket": "String",
  "postBackUri": "String"
}
```

