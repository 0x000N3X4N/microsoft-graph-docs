---
title: "List appRoleAssignments granted to a service principal"
description: "Retrieve the list of app role assignments granted to a service principal."
localization_priority: Priority
doc_type: apiPageType
ms.prod: "microsoft-identity-platform"
author: "davidmu1"
---

# List appRoleAssignments granted to a service principal

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Retrieve the list of [appRoleAssignment](../resources/approleassignment.md) that have been granted to a service principal.

App roles that are assigned to service principals are also known as [application permissions](https://docs.microsoft.com/azure/active-directory/develop/v2-permissions-and-consent#permission-types). Application permissions can be granted directly by creating app role assignments, or through a [consent experience](https://docs.microsoft.com/azure/active-directory/develop/application-consent-experience).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type      | Permissions (from least to most privileged)              |
|:--------------------|:---------------------------------------------------------|
|Delegated (work or school account) | Directory.Read.All, AppRoleAssignment.ReadWrite.All, Directory.ReadWrite.All, Directory.AccessAsUser.All  |
|Delegated (personal Microsoft account) | Not supported.    |
|Application | Directory.Read.All, AppRoleAssignment.ReadWrite.All, Directory.ReadWrite.All |

## HTTP request

<!-- { "blockType": "ignored" } -->
```http
GET /servicePrincipals/{id}/appRoleAssignments
```

## Optional query parameters

This method supports the [OData query parameters](/graph/query-parameters) to help customize the response.

To learn how to search for and filter app role assignments, see [supported filter patterns](../resources/approleassignment.md#supported-filter-patterns).

## Request headers

| Name           | Description                |
|:---------------|:---------------------------|
| Authorization  | Bearer {token}. Required.  |

## Request body

Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and a collection of [appRoleAssignment](../resources/approleassignment.md) objects in the response body.

## Example

### Request

The following is an example of a request to retrieve the app roles that have been assigned to a service principal.

<!-- {
  "blockType": "request",
  "name": "serviceprincipal_get_approleassignments"
}-->

```http
GET https://graph.microsoft.com/beta/servicePrincipals/{id}/appRoleAssignments
```

### Response

Here is an example of the response. 

> **Note:** The response object shown here might be shortened for readability. All the properties will be returned from an actual call.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.appRoleAssignment",
  "isCollection": true
} -->

```http
HTTP/1.1 200 OK
Content-type: application/json
Content-length: 306

{
  "value": [
    {
      "creationTimestamp": "2016-10-19T10:37:00Z",
      "id": "id-value",
      "principalDisplayName": "principalDisplayName-value",
      "principalId": "principalId-value",
      "principalType": "principalType-value",
      "resourceDisplayName": "resourceDisplayName-value"
    }
  ]
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!--
{
  "type": "#page.annotation",
  "description": "List appRoleAssignments",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}
-->
