---
title: "reviewSet resource type"
description: "PROVIDE DESCRIPTION HERE"
localization_priority: Normal
author: ""
ms.prod: ""
doc_type: "resourcePageType"
---

# reviewSet resource type

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

eDiscovery review sets are static set of electronically stored information collected for use in a litigation, investigation or regulatory request.

## Methods

| Method       | Return Type | Description |
|:-------------|:------------|:------------|
| [List](../api/ediscovery-reviewset-list.md) | [reviewSet](reviewset.md) collection | Get a collection of review sets. |
| [Get](../api/ediscovery-reviewset-get.md) | [reviewSet](reviewset.md) | Read properties and relationships of reviewSet object. |
| [Create](../api/ediscovery-reviewset-create.md) | [reviewSet](reviewset.md) | Create a new review set. |


## Properties

| Property     | Type        | Description |
|:-------------|:------------|:------------|
|createdBy| [identitySet](https://docs.microsoft.com/graph/api/resources/identityset) | The user who created the review set. |
|createdDateTime|DateTimeOffset| The datetime when the review set was created. The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 would look like this: `'2014-01-01T00:00:00Z'`|
|displayName|String| The review set name. Name is unique with a maximum limit of 64 characters. |
|id|String| The review set unique identifier. Read-only.|

## Relationships

| Relationship | Type        | Description |
|:-------------|:------------|:------------|
| Review set query |[reviewSetQuery](ediscovery-reviewset-query.md) collection| Read-only. Nullable.|

## JSON representation

The following is a JSON representation of the resource.

<!-- {
  "blockType": "resource",
  "optionalProperties": [

  ],
  "@odata.type": "microsoft.graph.reviewSet",
  "baseType": "",
  "keyProperty": "id"
}-->

```json
{
  "createdBy": {"@odata.type": "microsoft.graph.identitySet"},
  "createdDateTime": "String (timestamp)",
  "displayName": "String",
  "id": "String (identifier)"
}
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "reviewSet resource",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->