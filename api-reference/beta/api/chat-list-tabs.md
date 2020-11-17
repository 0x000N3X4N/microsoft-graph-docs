---
title: "List tabs in chat"
description: "Retrieve the list of tabs in the specified chat. "
author: "nkramer"
localization_priority: Normal
ms.prod: "microsoft-teams"
doc_type: apiPageType
---
 
# List tabs in chat
 
Namespace: microsoft.graph
 
[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]
 
Retrieve the list of [tabs](../resources/teamstab.md) in the specified [chat](../resources/chat.md) .

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type      | Permissions | 
|:--------------------|:---------------------------------|
|Delegated  | TeamsTab.Create, TeamsTab.ReadWrite.All  |
|Delegated  | TeamsTab.Read.All, TeamsTab.ReadWrite.All |
 
## HTTP request
<!-- { "blockType": "ignored" } -->

```http
GET /chats/{id}/tabs
```
 
## Optional query parameters
 
This method supports the $filter, $select, and $expand [OData query parameters](/graph/query-parameters) to help customize the response.
 
## Request headers
| Header       | Value |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |
 
## Response
If successful, this method returns a `200 OK` response code and collection of [tabs](../resources/teamstab.md) objects in the response body.
 
## Example

### Request
The following is an example of the request.
<!-- {
  "blockType": "request",
  "name": "List tabs in chat"
} -->

```http
GET /chats/{chatId}/tabs
```

### Response

The following is an example of the response.
<!-- 
{
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.chatMessage"
  } -->

```http
HTTP/1.1 200 OK
Content-type: application/json

{
  "@odata.context": "https://localhost:8200/beta/$metadata#chats/{chatId}/tabs",
  "@odata.count": 1,
  "value": [
    {
      "id": "62a07424-9c50-4adf-8931-c0038d7ef11e",
      "displayName": "My Awesome Tab",
      "webUrl": "https://teams.microsoft.com/l/chat/19%3ac2e36757ee744c569e70b385e6dd79b6%40thread.skype/tab%3a%3afd736d46-51ed-4c0b-9b23-e67ca354bb24?label=my%20%awesome%to%tab",
      "configuration": {
        "entityId": "fd3791c9-1e39-42b9-9e48-e9b1cbe54f99",
        "contentUrl": "https://www.example.com/",
        "removeUrl": "https://www.example.com/",
        "websiteUrl": "https://www.example.com/",
        "customPropertyInt": 1,
        "customPropertyBool": true,
        "customPropertyString": "value"
      }
     }
    ]  
}

```

### Example : List tabs in a chat

#### Request

The following example shows a request to list all chats.
<!-- {
  "blockType": "request",
  "name": "list-tabs in chat"
}-->

```http
GET /chat/19:75a0894119a0468caee5811901a75ffd@thread.tacv2/tabs
```

#### Response

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.chatMessage"
  } -->

The following is an example of the response.
```http
HTTP/1.1 200 OK
Content-type: application/json

{
  "@odata.context": "https://localhost:8200/beta/$metadata#chats/19:75a0894119a0468caee5811901a75ffd@thread.tacv2/tabs",
  "@odata.count": 1,
  "value": [
  {
    "id": "794f0e4e-4d10-4bb5-9079-3a465a629eff",
    "displayName": "Scrum Board",
    "webUrl": "https://teams.microsoft.com/l/chat/19:75a0894119a0468caee5811901a75ffd@thread.tacv2/tab%3a%3a794f0e4e-4d10-4bb5-9079-3a465a629eff?label=scrum%20tab",
    "configuration": {
      "entityId": "2DCA2E6C7A10415CAF6B8AB6661B3154",
      "contentUrl": "https://www.contoso.com/scrumsboards/",
      "websiteUrl": "https://www.contoso.com/scrumsboards/2DCA2E6C7A10415CAF6B8AB6661B3154",
      "removeUrl": "https://www.contoso.com/scrumsboards.2DCA2E6C7A10415CAF6B8AB6661B3154/uninstallTab"
    }
   }
  ]
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!--
{
  "type": "#page.annotation",
  "description": "List-tabs in chat",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": []
}
-->

