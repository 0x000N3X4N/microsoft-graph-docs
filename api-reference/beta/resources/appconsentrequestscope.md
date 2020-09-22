---
title: "appConsentRequestScope resource type"
description: "The appConsentRequestScope contains details of the dynamic permission scopes for which access is being requested."
author: "davidmu1"
localization_priority: Normal
ms.prod: "microsoft-identity-platform"
doc_type: resourcePageType
---

# appConsentRequestScope resource type

Namespace: microsoft.graph

The appConsentRequestScope contains details of the dynamic permission scopes for which access is being requested.

## Properties

| Property | Type | Description |
|:---|:---|:---|
| displayName | String | The name of the scope. |

## Relationships

None.

## JSON representation

The following is a JSON representation of the resource.
<!-- {
  "blockType": "resource",
  "@odata.type": "microsoft.graph.appConsentRequestScope"
}
-->
``` json
{
  "@odata.type": "#microsoft.graph.appConsentRequestScope",
  "displayName": "String"
}
```