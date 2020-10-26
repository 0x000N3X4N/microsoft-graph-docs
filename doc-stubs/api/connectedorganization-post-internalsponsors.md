---
title: "Create internalSponsors"
description: "Create a new directoryObject object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Create internalSponsors
Namespace: microsoft.graph

Create a new directoryObject object.

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
POST /identityGovernance/entitlementManagement/accessPackageResourceRequests/{accessPackageResourceRequestId}/requestor/connectedOrganization/internalSponsors
POST /identityGovernance/entitlementManagement/accessPackageResourceRequests/{accessPackageResourceRequestId}/requestor/connectedOrganization/externalSponsors
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [directoryObject](../resources/directoryobject.md) object.

The following table shows the properties that are required when you create the [directoryObject](../resources/directoryobject.md).

|Property|Type|Description|
|:---|:---|:---|
|id|String|**TODO: Add Description**|



## Response

If successful, this method returns a `201 Created` response code and a [directoryObject](../resources/directoryobject.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "create_directoryobject_from_"
}
-->
``` http
POST https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageResourceRequests/{accessPackageResourceRequestId}/requestor/connectedOrganization/internalSponsors
Content-Type: application/json
Content-length: 85

{
  "@odata.type": "#Microsoft.IGAELM.PDS.FrontEnd.ExternalModel.directoryObject"
}
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "Microsoft.IGAELM.PDS.FrontEnd.ExternalModel.directoryObject"
}
-->
``` http
HTTP/1.1 201 Created

Content-Type: application/json
{
  "@odata.type": "#Microsoft.IGAELM.PDS.FrontEnd.ExternalModel.directoryObject",
  "id": "f3256eaa-6eaa-f325-aa6e-25f3aa6e25f3"
}
```

