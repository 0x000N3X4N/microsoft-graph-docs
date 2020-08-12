---
title: "Get events"
description: "Read the properties and relationships of an event object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Get events
Namespace: microsoft.graph

Read the properties and relationships of an [event](../resources/event.md) object.

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
GET /groups/{groupsId}/events
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

If successful, this method returns a `200 OK` response code and an [event](../resources/event.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "get_event"
}
-->
``` http
GET https://graph.microsoft.com/beta/groups/{groupsId}/events
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.event"
}
-->
``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "value": {
    "@odata.type": "#microsoft.graph.event",
    "id": "d6ed394a-394a-d6ed-4a39-edd64a39edd6",
    "createdDateTime": "String (timestamp)",
    "lastModifiedDateTime": "String (timestamp)",
    "changeKey": "String",
    "categories": [
      "String"
    ],
    "transactionId": "String",
    "originalStartTimeZone": "String",
    "originalEndTimeZone": "String",
    "responseStatus": {
      "@odata.type": "microsoft.graph.responseStatus"
    },
    "uid": "String",
    "reminderMinutesBeforeStart": "Integer",
    "isReminderOn": "Boolean",
    "hasAttachments": "Boolean",
    "subject": "String",
    "body": {
      "@odata.type": "microsoft.graph.itemBody"
    },
    "bodyPreview": "String",
    "importance": "String",
    "sensitivity": "String",
    "start": {
      "@odata.type": "microsoft.graph.dateTimeTimeZone"
    },
    "originalStart": "String (timestamp)",
    "end": {
      "@odata.type": "microsoft.graph.dateTimeTimeZone"
    },
    "location": {
      "@odata.type": "microsoft.graph.location"
    },
    "locations": [
      {
        "@odata.type": "microsoft.graph.location"
      }
    ],
    "isAllDay": "Boolean",
    "isCancelled": "Boolean",
    "isOrganizer": "Boolean",
    "recurrence": {
      "@odata.type": "microsoft.graph.patternedRecurrence"
    },
    "responseRequested": "Boolean",
    "seriesMasterId": "String",
    "showAs": "String",
    "type": "String",
    "attendees": [
      {
        "@odata.type": "microsoft.graph.attendee"
      }
    ],
    "organizer": {
      "@odata.type": "microsoft.graph.recipient"
    },
    "webLink": "String",
    "onlineMeetingUrl": "String",
    "isOnlineMeeting": "Boolean",
    "onlineMeetingProvider": "String",
    "onlineMeeting": {
      "@odata.type": "microsoft.graph.onlineMeetingInfo"
    },
    "allowNewTimeProposals": "Boolean",
    "cancelledOccurrences": [
      "String"
    ],
    "occurrenceId": "String",
    "isDraft": "Boolean"
  }
}
```

