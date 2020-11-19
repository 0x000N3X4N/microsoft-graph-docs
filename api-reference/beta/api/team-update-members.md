---
title: "Update team member"
description: "Update the role of a member in a team."
author: "clearab"
doc_type: "apiPageType"
localization_priority: Normal
ms.prod: "microsoft-teams"
---

# Update team member

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Update the role of a [conversationMember](../resources/conversationmember.md) in a [team](../resources/team.md).

> [!NOTE]
> On channels, this operation is only supported on channels with a [channelMembershipType](../resources/enums.md#channelmembershiptype-values) of `private`. Calls with any other [channelMembershipType](../resources/enums.md#channelmembershiptype-values) will return a `400 Bad Request` response.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission Type|Permissions (from least to most privileged)|
|---------|-------------|
|Delegated (work or school account)| TeamMember.ReadWrite.All |
|Delegated (personal Microsoft account)|Not supported|
|Application|  TeamMember.ReadWrite.All |

## HTTP request

<!-- { "blockType": "ignored"} -->
```http
PATCH /teams/{team-Id}/members/{membership-Id}
```

## Request headers

| Header       | Value |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

## Request body

In the request body, supply the values for the relevant fields to update. Existing properties that are not included in the request body will maintain their previous values or be recalculated based on changes to other property values. For best performance, don't include existing values that haven't changed.

| Property   | Type |Description|
|:---------------|:--------|:----------|
|roles|string collection|The roles for that user. Must be "owner" or empty. Guest users must always have role "guest" and cannot change. |

## Response

If successful, this method returns a `200 OK` response code and a [conversationMember](../resources/conversationmember.md) object in the response body.

## Example

### Request

Here is an example of the request.

<!-- {
  "blockType": "request",
  "name": "update_team_member"
} -->

```http
PATCH https://graph.microsoft.com/v1.0/teams/{team-Id}/members/{membership-Id}

```

### Response

Here is an example of the response.

>**Note:** The response object shown here might be shortened for readability. All the properties will be returned from an actual call.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.conversationMember"
} -->
```http
HTTP/1.1 200 OK

{
    "id":"id",
    "roles": ["owner"],
    "userId":"7051f984-682e-4a08-a6b2-df82fe7d9fe1",
    "displayName":"John Doe",
    "email":"johnDoe@yourTenant.com"
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!--
{
  "type": "#page.annotation",
  "description": "update member's role in team",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}
-->

<!-- ## See also

 [Update the role of a member in a channel](../api/channel-update-members.md) -->
