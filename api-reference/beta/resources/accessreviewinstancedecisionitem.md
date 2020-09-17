---
title: "accessReviewInstanceDecisionItem resource type"
description: "In the Azure AD access reviews feature, the `accessReviewInstanceDecisionItem` represents a decision on a user's access on an `accessReviewInstance`.  "
localization_priority: Normal
author: "isabelleatmsft"
ms.prod: "microsoft-identity-platform"
doc_type: resourcePageType
---

# accessReviewInstanceDecisionItem resource type

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Represents an Azure AD [access review](accessreviews-root.md) decision on an instance of a review.

## Methods

| Method		   | Return Type	|Description|
|:---------------|:--------|:----------|



## Properties
| Property                  | Type                                |  Description |
| :-------------------------| :---------------------------------- | :---------- |
| `id`                            |`String`                      | ID of the decision                                                                                     |
| `accessReviewId`                |`String`                      | ID of the review                                                                                       |
| `reviewedBy`                    |`microsoft.graph.userIdentity`| Reviewer user ID                                                                                       |
| `reviewedDate`                  |`DateTimeOffset`              | DateTime when review occurred                                                                     |
| `decision`                      |`String`                      | Result of the review                                                                                   |
| `justification`                 |`String`                      | Review decision justification                                                                          |
| `appliedBy`                     |`microsoft.graph.userIdentity`| User ID of the user who applied the decision                                                           |
| `appliedDateTime`               |`DateTimeOffset`              | DateTime when approval decision was applied                                                           |
| `applyResult`                   |`String`                      | Result of applying the decision. Values are: `NotApplied` `Success` `Failed` `NotFound` `NotSupported`.                      |
| `recommendation`          |`String`                      | System-generated recommendation for the approval decision. Values are: `Approve` `Deny` `NotAvailable`. |
| `target`                       |`microsoft.graph.accessReviewInstanceDecisionItemTarget`                      | Target of this specific decision. Decision Targets can be of different types – each one with its own specific properties. |

## Relationships

| Relationship | Type	|Description|
|:---------------|:--------|:----------|
| `instance`               |[accessReviewInstance](accessreviewinstance.md)          | There is exactly one `accessReviewInstance` associated with each decision. The instance is the parent of the decision item, representing the recurrence of an access review the decision is made on. |


## JSON representation

Here is a JSON representation of the resource.

<!-- {
  "blockType": "resource",
  "keyProperty": "id",
  "optionalProperties": [

  ],
  "@odata.type": "microsoft.graph.accessReview"
}-->

```json
{
 "id": "string (identifier)",
 "displayName": "string",
 "startDateTime": "string (timestamp)",
 "endDateTime": "string (timestamp)",
 "status": "string",
 "scope": "microsoft.graph.accessReviewScope",
 "decisions": "Collection(microsoft.graph.accessReviewInstanceDecisionItem)",
 "definition":"microsoft.graph.accessReviewScheduleDefinition"
}
```

<!--
{
  "type": "#page.annotation",
  "description": "accessReview resource",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": []
}
-->
