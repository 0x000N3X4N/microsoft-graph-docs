---
title: "List accessReviewScheduleDefinitions"
description: "Get a list of the accessReviewScheduleDefinition objects and their properties."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# List accessReviewScheduleDefinitions
Namespace: microsoft.graph

Get a list of the [accessReviewScheduleDefinition](../resources/accessreviewscheduledefinition.md) objects and their properties.

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
GET /identityGovernance/accessReviews/definitions
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

If successful, this method returns a `200 OK` response code and a collection of [accessReviewScheduleDefinition](../resources/accessreviewscheduledefinition.md) objects in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "get_accessreviewscheduledefinition"
}
-->
``` http
GET https://graph.microsoft.com/beta/identityGovernance/accessReviews/definitions
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "Collection(microsoft.graph.accessReviewScheduleDefinition)"
}
-->
``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "value": [
    {
      "@odata.type": "#microsoft.graph.accessReviewScheduleDefinition",
      "id": "26a0f8bd-f8bd-26a0-bdf8-a026bdf8a026",
      "displayName": "String",
      "createdDateTime": "String (timestamp)",
      "lastModifiedDateTime": "String (timestamp)",
      "status": "String",
      "descriptionForAdmins": "String",
      "descriptionForReviewers": "String",
      "createdBy": {
        "@odata.type": "microsoft.graph.userIdentity"
      },
      "scope": {
        "@odata.type": "microsoft.graph.accessReviewScope"
      },
      "reviewers": [
        {
          "@odata.type": "microsoft.graph.accessReviewReviewerScope"
        }
      ],
      "backupReviewers": [
        {
          "@odata.type": "microsoft.graph.accessReviewReviewerScope"
        }
      ],
      "instanceEnumerationScope": {
        "@odata.type": "microsoft.graph.accessReviewScope"
      },
      "settings": {
        "@odata.type": "microsoft.graph.accessReviewScheduleSettings"
      }
    }
  ]
}
```

