---
title: "Add app to chat"
description: "API to install an app to chat."
author: "nkramer"
localization_priority: Priority
ms.prod: "microsoft-teams"
doc_type: apiPageType
---

# Add app to chat

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Installs an [app](../resources/teamsapp.md) to the specified [chat](../resources/chat.md).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type      | Permissions (from least to most privileged)              |
|:--------------------|:---------------------------------------------------------|
|Delegated (work or school account) | TeamsAppInstallation.ReadWriteSelfForChat, TeamsAppInstallation.ReadWriteForChat |
|Delegated (personal Microsoft account) | Not supported.    |
|Application | TeamsAppInstallation.ReadWriteSelfForChat.All, TeamsAppInstallation.ReadWriteForChat.All |

## HTTP request
<!-- { "blockType": "ignored" } -->
```http
POST /chats/{chatId}/installedApps
```

## Request body

The request body should contain the ID of the existing catalog app to be added.

## Response

201 Created

## Example

### Request

The following is an example of the request.

<!-- {
  "blockType": "request",
  "name": "add_teamsApp"
}-->

```http
POST https://graph.microsoft.com/beta/chats/19:ea28e88c00e94c7786b065394a61f296@thread.v2/installedApps

{
"teamsApp@odata.bind":"https://graph.microsoft.com/beta/appCatalogs/teamsApps/12345678-9abc-def0-123456789a"
}
```

### Response

```http
HTTP/1.1 201 Created

Content-Type: application/json
```

<!--{
  "value": {
    "@odata.type": "#microsoft.graph.chat",
    "id": "4c54cdc2-6f55-4587-a7cc-c7280997b04f",
    "topic": "Add app to chat",
    "createdDateTime": "2020-10-27 23:52:29",
    "lastUpdatedDateTime": "2020-10-27 23:52:29"
  }
}-->
