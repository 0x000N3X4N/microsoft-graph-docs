---
title: "userAccountInformation resource type"
description: "**TODO: Add Description**"
author: "**TODO: Provide Github Name. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
localization_priority: Normal
ms.prod: "**TODO: Add MS prod. See [topic-level metadata reference](https://msgo.azurewebsites.net/add/document/guidelines/metadata.html#topic-level-metadata)**"
doc_type: resourcePageType
---

# userAccountInformation resource type

Namespace: microsoft.graph

**TODO: Add Description**


Inherits from [itemFacet](../resources/itemfacet.md).

## Methods
|Method|Return type|Description|
|:---|:---|:---|
|[List account](../api/profile-list-account.md)|[userAccountInformation](../resources/useraccountinformation.md) collection|Get the userAccountInformations from the account navigation property.|
|[Create account](../api/profile-post-account.md)|[userAccountInformation](../resources/useraccountinformation.md)|Create a new account object.|
|[Update account](../api/profile-update-account.md)|[userAccountInformation](../resources/useraccountinformation.md)|Update the properties of an account object.|
|[Get account](../api/profile-get-useraccountinformation.md)|[userAccountInformation](../resources/useraccountinformation.md)|Read the properties and relationships of a [userAccountInformation](../resources/useraccountinformation.md) object.|
|[Delete account](../api/profile-delete-account.md)|None|Delete a [userAccountInformation](../resources/useraccountinformation.md) object.|
|[List userAccountInformations](../api/useraccountinformation-list.md)|[userAccountInformation](../resources/useraccountinformation.md) collection|Get a list of the [userAccountInformation](../resources/useraccountinformation.md) objects and their properties.|
|[Create userAccountInformation](../api/useraccountinformation-create.md)|[userAccountInformation](../resources/useraccountinformation.md)|Create a new [userAccountInformation](../resources/useraccountinformation.md) object.|
|[Get userAccountInformation](../api/useraccountinformation-get.md)|[userAccountInformation](../resources/useraccountinformation.md)|Read the properties and relationships of a [userAccountInformation](../resources/useraccountinformation.md) object.|
|[Update userAccountInformation](../api/useraccountinformation-update.md)|[userAccountInformation](../resources/useraccountinformation.md)|Update the properties of a [userAccountInformation](../resources/useraccountinformation.md) object.|
|[Delete userAccountInformation](../api/useraccountinformation-delete.md)|None|Deletes a [userAccountInformation](../resources/useraccountinformation.md) object.|

## Properties
|Property|Type|Description|
|:---|:---|:---|
|ageGroup|String|**TODO: Add Description**|
|allowedAudiences|allowedAudiences|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md). Possible values are: `me`, `family`, `contacts`, `groupMembers`, `organization`, `federatedOrganizations`, `everyone`, `unknownFutureValue`.|
|countryCode|String|**TODO: Add Description**|
|createdBy|[identitySet](../resources/identityset.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|createdDateTime|DateTimeOffset|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|id|String|**TODO: Add Description** Inherited from [entity](../resources/entity.md)|
|inference|[inferenceData](../resources/inferencedata.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|lastModifiedBy|[identitySet](../resources/identityset.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|lastModifiedDateTime|DateTimeOffset|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|preferredLanguageTag|[localeInfo](../resources/localeinfo.md)|**TODO: Add Description**|
|source|[personDataSource](../resources/persondatasource.md)|**TODO: Add Description** Inherited from [itemFacet](../resources/itemfacet.md)|
|userPrincipalName|String|**TODO: Add Description**|

## Relationships
None.

## JSON representation
The following is a JSON representation of the resource.
<!-- {
  "blockType": "resource",
  "keyProperty": "id",
  "@odata.type": "microsoft.graph.userAccountInformation",
  "baseType": "microsoft.graph.itemFacet",
  "openType": false
}
-->
``` json
{
  "@odata.type": "#microsoft.graph.userAccountInformation",
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
  "ageGroup": "String",
  "countryCode": "String",
  "preferredLanguageTag": {
    "@odata.type": "microsoft.graph.localeInfo"
  },
  "userPrincipalName": "String"
}
```

