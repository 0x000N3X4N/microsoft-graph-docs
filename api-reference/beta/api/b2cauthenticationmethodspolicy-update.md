---
title: "Update b2cAuthenticationMethodsPolicy"
description: "Retrieve the properties and relationships of an b2cAuthenticationMethodsPolicy object."
localization_priority: Priority
author: "namkedia"
ms.prod: "microsoft-identity-platform"
doc_type: "apiPageType"
---

# Update b2cAuthenticationMethodsPolicy

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Update the properties of an [b2cAuthenticationMethodsPolicy](../resources/b2cauthenticationmethodspolicy.md) object.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions|
|:---------------------------------------|:---------------|
| Delegated (work or school account)     | Policy.ReadWrite.AuthenticationMethod|
| Delegated (personal Microsoft account) | Policy.ReadWrite.AuthenticationMethod|
| Application                            | Policy.ReadWrite.AuthenticationMethod|

## HTTP request

<!-- { "blockType": "ignored" } -->

```http
PATCH https://graph.microsoft.com/beta/policies/b2cAuthenticationMethodsPolicy
```

## Optional query parameters

This method does not support optional query parameters to customize the response.

## Request headers

|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body

In the request body, you can supply a JSON representation of the [b2cAuthenticationMethodsPolicy](../resources/b2cauthenticationmethodspolicy.md) object (but is not required.)

The following table shows the properties that are required when you update the [b2cAuthenticationMethodsPolicy](../resources/b2cauthenticationmethodspolicy.md).

| Property     | Type        | Description |
|:-------------|:------------|:------------|
|isPhoneOneTimePasswordAuthenticationEnabled|Boolean|This property lets the tenant admin configure if the phone one time password authentication method is enabled|
|isEmailPasswordAuthenticationEnabled|Boolean|This property lets the tenant admin configure if the email and password authentication method is enabled|
|isUserNameAuthenticationEnabled|Boolean|This property lets the tenant admin configure if the user name and password authentication method is enabled|

## Response

If successful, this method returns a `204 No Content` response code and an empty response body.

## Examples

### Request

The following is an example of the request.

<!-- {
  "blockType": "request",
  "name": "patch_b2cauthenticationmethodspolicy"
}-->

```msgraph-interactive
PATCH https://graph.microsoft.com/beta/policies/b2cauthenticationmethodspolicy
```

### Response

The following is an example of the response.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.b2cauthenticationmethodspolicy"
} -->

```http
HTTP/1.1 204 NO CONTENT
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "Update b2cauthenticationmethodspolicy",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->
