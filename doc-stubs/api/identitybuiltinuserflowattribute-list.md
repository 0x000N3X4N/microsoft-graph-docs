---
title: "List identityBuiltInUserFlowAttributes"
description: "Get a list of the identityBuiltInUserFlowAttribute objects and their properties."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# List identityBuiltInUserFlowAttributes
Namespace: microsoft.graph

Get a list of the [identityBuiltInUserFlowAttribute](../resources/identitybuiltinuserflowattribute.md) objects and their properties.

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
GET ** Collection URI for Microsoft.Cpim.Api.DataModels.identityBuiltInUserFlowAttribute not found
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

If successful, this method returns a `200 OK` response code and a collection of [identityBuiltInUserFlowAttribute](../resources/identitybuiltinuserflowattribute.md) objects in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "get_identitybuiltinuserflowattribute"
}
-->
``` http
GET https://graph.microsoft.com/beta** Collection URI for Microsoft.Cpim.Api.DataModels.identityBuiltInUserFlowAttribute not found
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "Collection(Microsoft.Cpim.Api.DataModels.identityBuiltInUserFlowAttribute)"
}
-->
``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "value": [
    {
      "@odata.type": "#Microsoft.Cpim.Api.DataModels.identityBuiltInUserFlowAttribute",
      "id": "6ec203f4-03f4-6ec2-f403-c26ef403c26e",
      "displayName": "String",
      "description": "String",
      "userFlowAttributeType": "String",
      "dataType": "String"
    }
  ]
}
```

