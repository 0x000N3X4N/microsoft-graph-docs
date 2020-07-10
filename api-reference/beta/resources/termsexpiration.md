---
title: "termsExpiration complex type"
description: "Represents the settings for tenant's customizable terms of use agreement that is created and managed with Azure Active Directory (Azure AD)."
localization_priority: Normal
ms.prod: "microsoft-identity-platform"
author: "raprakasMSFT"
doc_type: "resourcePageType"
---


# termsExpiration complex type

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

The **termsExpiration** complex type provides additional settings when setting the scheduled expiration of the agreement.

## Properties

| Property                     | Type                      | Description |
| :--------------------------- | :------------------------ | :---------- |
| `startDateTime`|`DateTimeOffset`                | The DateTime when the agreement is set to expire for all users. The Timestamp type represents date and time information using ISO 8601 format and is always in UTC time. For example, midnight UTC on Jan 1, 2014 would look like this: '2014-01-01T00:00:00Z'.|
| `frequency`|`Duration`       | This represents the frequency at which the terms will expire, after its first expiration as set in 'startDateTime'. The value is represented in ISO 8601 format for durations.|

## JSON representation

The following is a JSON representation of termsExpiration.

<!-- {
  "blockType": "resource",
  "optionalProperties": [

  ],
  "@odata.type": "microsoft.graph.termsExpiration",
  "baseType": ""
}-->

```json
{
   "startDateTime": "2018-10-01T00:00:00.0000000Z",
   "frequency": ""
}
```

<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79
2015-10-25 14:57:30 UTC -->
<!--
{
  "type": "#page.annotation",
  "description": "termsExpiration complex type",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": []
}
-->
