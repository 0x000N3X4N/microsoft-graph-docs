---
title: "Update scopedRoleMembership"
description: "Update the properties of a scopedRoleMembers object."
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: apiPageType
---

# Update scopedRoleMembership
Namespace: microsoft.graph

Update the properties of a scopedRoleMembers object.

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
PATCH /administrativeUnits/{administrativeUnitsId}/scopedRoleMembers
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body
In the request body, supply a JSON representation of the [scopedRoleMembership](../resources/scopedrolemembership.md) object.

The following table shows the properties that are required when you update the [scopedRoleMembership](../resources/scopedrolemembership.md).

|Property|Type|Description|
|:---|:---|:---|
|id|String|**TODO: Add Description**|
|roleId|String|**TODO: Add Description**|
|administrativeUnitId|String|**TODO: Add Description**|
|roleMemberInfo|[identity](../resources/identity.md)|**TODO: Add Description**|



## Response

If successful, this method returns a `200 OK` response code and an updated [scopedRoleMembership](../resources/scopedrolemembership.md) object in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "update_scopedrolemembers"
}
-->
``` http
PATCH https://graph.microsoft.com/beta/administrativeUnits/{administrativeUnitsId}/scopedRoleMembers
Content-Type: application/json
Content-length: 198

{
  "@odata.type": "#microsoft.graph.scopedRoleMembership",
  "roleId": "String",
  "administrativeUnitId": "String",
  "roleMemberInfo": {
    "@odata.type": "microsoft.graph.identity"
  }
}
```


### Response
**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true
}
-->
``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "@odata.type": "#microsoft.graph.scopedRoleMembership",
  "id": "0a0e9239-9239-0a0e-3992-0e0a39920e0a",
  "roleId": "String",
  "administrativeUnitId": "String",
  "roleMemberInfo": {
    "@odata.type": "microsoft.graph.identity"
  }
}
```

