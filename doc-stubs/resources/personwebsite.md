---
title: "personWebsite resource type"
description: "**TODO: Add Description**"
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: resourcePageType
---

# personWebsite resource type

Namespace: microsoft.graph

**TODO: Add Description**


Inherits from [itemFacet](../resources/itemfacet.md).

## Methods
|Method|Return type|Description|
|:---|:---|:---|
|[List websites](../api/profile-list-websites.md)|[personWebsite](../resources/personwebsite.md) collection|Get the personWebsites from the websites navigation property.|
|[Create websites](../api/profile-post-websites.md)|[personWebsite](../resources/personwebsite.md)|Create a new websites object.|
|[Update websites](../api/profile-update-websites.md)|[personWebsite](../resources/personwebsite.md)|Update the properties of a websites object.|
|[Get websites](../api/profile-get-personwebsite.md)|[personWebsite](../resources/personwebsite.md)|Read the properties and relationships of a [personWebsite](../resources/personwebsite.md) object.|
|[Delete websites](../api/profile-delete-websites.md)|None|Delete a [personWebsite](../resources/personwebsite.md) object.|
|[List personWebsites](../api/personwebsite-list.md)|[personWebsite](../resources/personwebsite.md) collection|Get a list of the [personWebsite](../resources/personwebsite.md) objects and their properties.|
|[Create personWebsite](../api/personwebsite-create.md)|[personWebsite](../resources/personwebsite.md)|Create a new [personWebsite](../resources/personwebsite.md) object.|
|[Get personWebsite](../api/personwebsite-get.md)|[personWebsite](../resources/personwebsite.md)|Read the properties and relationships of a [personWebsite](../resources/personwebsite.md) object.|
|[Update personWebsite](../api/personwebsite-update.md)|[personWebsite](../resources/personwebsite.md)|Update the properties of a [personWebsite](../resources/personwebsite.md) object.|
|[Delete personWebsite](../api/personwebsite-delete.md)|None|Deletes a [personWebsite](../resources/personwebsite.md) object.|

## Properties
|Property|Type|Description|
|:---|:---|:---|
|allowedAudiences|allowedAudiences|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md). Possible values are: `me`, `family`, `contacts`, `groupMembers`, `organization`, `federatedOrganizations`, `everyone`, `unknownFutureValue`.|
|categories|String collection|**TODO: Add Description**|
|createdBy|[identitySet](../resources/identityset.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|createdDateTime|DateTimeOffset|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|description|String|**TODO: Add Description**|
|displayName|String|**TODO: Add Description**|
|id|String|**TODO: Add Description** Inherited from [entity](../resources/entity.md)|
|inference|[inferenceData](../resources/inferencedata.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|lastModifiedBy|[identitySet](../resources/identityset.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|lastModifiedDateTime|DateTimeOffset|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|source|[personDataSource](../resources/persondatasource.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|webUrl|String|**TODO: Add Description**|

## Relationships
None.

## JSON representation
The following is a JSON representation of the resource.
<!-- {
  "blockType": "resource",
  "keyProperty": "id",
  "@odata.type": "microsoft.graph.personWebsite",
  "baseType": "microsoft.graph.itemFacet",
  "openType": false
}
-->
``` json
{
  "@odata.type": "#microsoft.graph.personWebsite",
  "id": "String (identifier)",
  "allowedAudiences": "String",
  "inference": {
    "@odata.type": "microsoft.graph.inferenceData"
  },
  "createdDateTime": "String (timestamp)",
  "createdBy": {
    "@odata.type": "microsoft.graph.identitySet"
  },
  "lastModifiedDateTime": "String (timestamp)",
  "lastModifiedBy": {
    "@odata.type": "microsoft.graph.identitySet"
  },
  "source": {
    "@odata.type": "microsoft.graph.personDataSource"
  },
  "categories": [
    "String"
  ],
  "description": "String",
  "displayName": "String",
  "webUrl": "String"
}
```

