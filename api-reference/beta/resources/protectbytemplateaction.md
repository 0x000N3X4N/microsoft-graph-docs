---
title: "protectByTemplateAction resource type"
description: "Indicates that the information should be protected by RMS template."
localization_priority: Normal
author: "tommoser"
ms.prod: "microsoft.informationprotection"
doc_type: "resourcePageType"
---

# protectByTemplateAction resource type

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

`protectionByTemplateAction` may be returned by [evaluateApplication](../api/informationprotection-evaluateApplication.md) or [evaluateClassificationResults](../api/informationprotection-evaluateClassificationResults.md) if the resulting label has been configured to apply protection. The consuming application must read the templateId from the result and then use a client library, such as the Microsoft Information Protection SDK, to apply protection via Azure Information Protection.

## Properties

| Property   | Type   | Description                                                                        |
| :--------- | :----- | :--------------------------------------------------------------------------------- |
| templateId | String | The GUID of the Azure Information Protection template to apply to the information. |

## JSON representation

The following is a JSON representation of the resource.

<!-- {
  "blockType": "resource",
  "optionalProperties": [

  ],
  "@odata.type": "microsoft.graph.protectByTemplateAction",
  "baseType": "microsoft.informationProtection.informationProtectionAction"
}-->

```json
{
  "templateId": "String"
}
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "protectByTemplateAction resource",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->