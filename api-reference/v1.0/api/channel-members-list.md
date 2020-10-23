---
title: "List member from a channel"
description: "List member from a channel."
author: "laujan"
localization_priority: Priority
ms.prod: "microsoft-teams"
doc_type: apiPageType
---

# List member from a channel

Namespace: microsoft.graph

Retrieve a [conversationMember](../resources/conversationmember.md) from a [channel](../resources/channel.md).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission Type|Permissions (from least to most privileged)|
|---------|-------------|
|Delegated (work or school account)|ChannelMember.Read.All, ChannelMember.ReadWrite, Group.Read.All, Group.ReadWrite.All, Directory.Read.All, Directory.ReadWrite.All|
|Delegated (personal Microsoft account)|Not supported.|
|Application|Member.Read.Group*, ChannelMember.Read.All, ChannelMember.ReadWrite.All, Group.Read.All, Group.ReadWrite.All, Directory.Read.All, Directory.ReadWrite.All |

> **Note**: Permissions marked with * use [resource-specific consent](https://aka.ms/teams-rsc).

> [!NOTE]
> Before calling this API with application permissions, you must request access. For details, see [Protected APIs in Microsoft Teams](/graph/teams-protected-apis).

## HTTP request
<!-- { "blockType": "ignored" } -->
```http
GET /teams/{id}/channels/{id}/members/{id}
```

## Optional query parameters

This operation does not support the [OData query parameters](/graph/query-parameters) to customize the response.

## Request headers

| Header       | Value |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

## Request body

Do not supply a request body for this method.

## Response

If successful, this method returns a `200 OK` response code and a [conversationMember](../resources/conversationmember.md) object in the response body.

## Example

### Request

Here is an example of the request.

<!-- {
  "blockType": "request",
  "name": "list_member"
}-->

```msgraph-interactive
GET https://graph.microsoft.com/V1.0/channels/{id}/members/{id}
```

### Response

Here is an example of the response.

>**Note:** The response object shown here might be shortened for readability. All the properties will be returned from an actual call.
<!-- {
  "blockType": "response",
  "truncated": true,
  "name": "list_member",
  "@odata.type": "microsoft.graph.conversationMember"
} -->
```http
HTTP/1.1 200 OK
Content-type: application/json
Content-length: 201

{
  "id": "id-value",
  "displayName": "display-name-value"
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!--
{
  "type": "#page.annotation",
  "description": "conversation: member list",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}
-->
