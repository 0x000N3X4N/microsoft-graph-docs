---
title: "Update provisioningPolicies"
description: "Update the properties of a provisioningPolicies object."
author: "jiajyang"
localization_priority: Normal
ms.prod: "microsoft_cloudpc"
doc_type: apiPageType
---

# Update provisioningPolicies

Namespace: microsoft.graph

Update the properties of a provisioningPolicies object.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

|Permission type|Permissions (from most to least privileged)|
|:---|:---|
|Delegated (work or school account)|CloudPC.ReadWrite.All|
|Delegated (personal Microsoft account)|Not supported.|
|Application|Not supported.|

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->

``` http
PATCH /deviceManagement/virtualEndpoint/provisioningPolicies/{id}
```

## Request headers

|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body

In the request body, supply a JSON representation of the [cloudPcProvisioningPolicy](../resources/cloudpcprovisioningpolicy.md) object.

The following table shows the properties that are required when you create the [cloudPcProvisioningPolicy](../resources/cloudpcprovisioningpolicy.md).

|Property|Type|Description|
|:---|:---|:---|
|id|String|The provisioning policy id. Inherited from [entity](../resources/entity.md)|
|displayName|String|The provisioning policy display name|
|description|String|The provisioning policy description|
|onPremisesConnectionId|String|Id of the cloudPcOnPremisesConnection that indicates the virtual network that will enable Cloud PCs to have network connectivity and the domain that the Cloud PCs should join|
|imageId|String|Id of the OS Image to provision Cloud PCs with. For gallery type image, the id is of {publisher_offer_sku} format|
|imageDisplayName|String|Display name of the OS Image to provision Cloud PCs with|
|imageType|cloudPcProvisioningPolicyImageType|Type of the OS Image to provision Cloud PCs with. The type can be gallery or custom. Possible values are: `gallery`, `custom`.|

## Response

If successful, this method returns a `200 OK` response code and an updated [cloudPcProvisioningPolicy](../resources/cloudpcprovisioningpolicy.md) object in the response body.

## Examples

### Request

<!-- {
  "blockType": "request",
  "name": "update_provisioningpolicies"
}
-->

``` http
PATCH https://graph.microsoft.com/beta/deviceManagement/virtualEndpoint/provisioningPolicies/{id}
Content-Type: application/json
Content-length: 245

{
  "@odata.type": "#microsoft.graph.cloudPcProvisioningPolicy",
  "displayName": "HR provisioning policy",
  "description": "Provisioning policy for India HR employees",
  "onPremisesConnectionId": "4e47d0f6-6f77-44f0-8893-c0fe1701b553",
  "imageId": "53a93bfd-2006-4b76-8f30-5c0f60988105",
  "imageDisplayName": "Custom image name",
  "imageType": "Custom"
}
```

### Response

**Note:** The response object shown here might be shortened for readability.
<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.cloudPcProvisioningPolicy"
}
-->

``` http
HTTP/1.1 200 OK

Content-Type: application/json
{
  "@odata.type": "#microsoft.graph.cloudPcProvisioningPolicy",
  "id": "8931f750-f750-8931-50f7-318950f73189",
  "displayName": "HR provisioning policy",
  "description": "Provisioning policy for India HR employees",
  "onPremisesConnectionId": "4e47d0f6-6f77-44f0-8893-c0fe1701b553",
  "imageId": "53a93bfd-2006-4b76-8f30-5c0f60988105",
  "imageDisplayName": "Custom image name",
  "imageType": "customer"
}
```
