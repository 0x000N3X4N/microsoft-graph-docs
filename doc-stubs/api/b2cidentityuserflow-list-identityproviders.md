---
title: "List identityProviders"
description: "Get the IdentityProvider resources from the identityProviders navigation property."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# List identityProviders
Namespace: microsoft.graph

Get the IdentityProvider resources from the identityProviders navigation property.

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
GET /identity/b2cUserFlows/{b2cIdentityUserFlowId}/identityProviders
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

If successful, this method returns a `200 OK` response code and a collection of [IdentityProvider](../resources/identityprovider.md) objects in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "get_identityprovider"
}
-->
``` http
GET https://graph.microsoft.com/beta/identity/b2cUserFlows/{b2cIdentityUserFlowId}/identityProviders
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "Collection(Microsoft.Cpim.Api.DataModels.IdentityProvider)"
}
-->
``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "value": [
    {
      "@odata.type": "#Microsoft.Cpim.Api.DataModels.IdentityProvider"
    }
  ]
}
```

