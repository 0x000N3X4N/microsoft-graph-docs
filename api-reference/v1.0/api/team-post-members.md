---
title: "Add members to team"
description: "Add a new member to a team."
author: "nkramer"
localization_priority: Priority
ms.prod: "microsoft-teams"
doc_type: apiPageType
---

# Add members to team
Namespace: microsoft.graph

Add a new [conversationMember](../resources/conversationmember.md) to a [team](../resources/team.md).

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from most to least privileged)|
|:---|:---|
|Delegated (work or school account)| TeamMember.ReadWrite.All |
|Delegated (personal Microsoft account) | Not supported.    |
|Application| TeamMember.ReadWrite.All |

> **Note**: Permissions marked with * use [resource-specific consent]( https://aka.ms/teams-rsc).

## HTTP request

<!--
{
  "blockType": "ignored"
}
-->

``` http
POST /teams/{team-Id}/members
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [conversationMember](../resources/conversationmember.md) object.

## Response

If successful, this method returns a `201 Created` response code and a [conversationMember](../resources/conversationmember.md) object in the response body.

For best results, stagger calls with a 2 second buffer.

## Examples

### Request

<!--
{
  "blockType": "request",
  "name": "add members to team"
}
-->

``` http
POST https://graph.microsoft.com/v1.0/teams/id/members

{
  "@odata.type": "#microsoft.graph.aadUserConversationMember",
  "user@odata.bind": "https://graph.microsoft.com/v1.0/users('7051f984-682e-4a08-a6b2-df82fe7d9fe1')",
  "roles": [],
   "roles": ["owner"]
}
```

### Response
**Note:** The response object shown here might be shortened for readability.
<!--
{
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.conversationMember"
}
-->

``` http
HTTP/1.1 200 OK

{
    "@odata.type": "#microsoft.graph.aadUserConversationMember",
    "id": "3c02af05-9312-4966-bc84-c1a0818791c4",
    "roles": [],
    "userId": "7051f984-682e-4a08-a6b2-df82fe7d9fe1",
    "displayName": "George Washington",
    "email": "geowa@contoso.com"
}
```

<!--
{
  "type": "#page.annotation",
  "description": "add members to team",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}
-->

// ## See also

// [Add channel member](../api/channel-add-members.md)
