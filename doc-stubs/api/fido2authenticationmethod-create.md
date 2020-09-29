---
title: "Create fido2AuthenticationMethod"
description: "Create a new fido2AuthenticationMethod object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Create fido2AuthenticationMethod
Namespace: microsoft.graph

Create a new [fido2AuthenticationMethod](../resources/fido2authenticationmethod.md) object.

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
POST /user/authentication/fido2Methods
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [fido2AuthenticationMethod](../resources/fido2authenticationmethod.md) object.

The following table shows the properties that are required when you create the [fido2AuthenticationMethod](../resources/fido2authenticationmethod.md).

|Property|Type|Description|
|:---|:---|:---|
|id|String|**TODO: Add Description** Inherited from [authenticationMethod](../resources/authenticationmethod.md)|
|displayName|String|**TODO: Add Description**|
|creationDateTime|DateTimeOffset|**TODO: Add Description**|
|aaGuid|String|**TODO: Add Description**|
|model|String|**TODO: Add Description**|
|attestationCertificates|String collection|**TODO: Add Description**|
|attestationLevel|attestationLevel|**TODO: Add Description**. Possible values are: `attested`, `notAttested`, `unknownFutureValue`.|



## Response

If successful, this method returns a `201 Created` response code and a [fido2AuthenticationMethod](../resources/fido2authenticationmethod.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "create_fido2authenticationmethod_from_"
}
-->
``` http
POST https://graph.microsoft.com/beta/user/authentication/fido2Methods
Content-Type: application/json
Content-length: 285

{
  "@odata.type": "#microsoft.strongAuthentication.fido2AuthenticationMethod",
  "displayName": "String",
  "creationDateTime": "String (timestamp)",
  "aaGuid": "String",
  "model": "String",
  "attestationCertificates": [
    "String"
  ],
  "attestationLevel": "String"
}
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.strongAuthentication.fido2AuthenticationMethod"
}
-->
``` http
HTTP/1.1 201 Created

Content-Type: application/json
{
  "@odata.type": "#microsoft.strongAuthentication.fido2AuthenticationMethod",
  "id": "79846026-6026-7984-2660-847926608479",
  "displayName": "String",
  "creationDateTime": "String (timestamp)",
  "aaGuid": "String",
  "model": "String",
  "attestationCertificates": [
    "String"
  ],
  "attestationLevel": "String"
}
```

