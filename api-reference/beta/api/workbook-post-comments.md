---
title: "Create workbookComment"
description: "Create a new workbookComment object."
localization_priority: Normal
author: "grangeryy"
ms.prod: "excel"
doc_type: "apiPageType"
---

# Create workbookComment

Create a new workbookComment object.

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged) |
|:---------------------------------------|:--------------------------------------------|
| Delegated (work or school account)     | Files.ReadWrite |
| Delegated (personal Microsoft account) | Not supported. |
| Application                            | Not supported. |

## HTTP request

<!-- { "blockType": "ignored" } -->

```http
POST /drive/root/workbook/comments
POST /me/drive/root/workbook/comments
POST /workbooks/{id}/workbook/comments
```

## Request headers

| Name          | Description   |
|:--------------|:--------------|
| Authorization | Bearer {token} |

## Request body

In the request body, supply a JSON representation of a [workbookComment](../resources/workbookcomment.md) object.

## Response

If successful, this method returns a `201 Created` response code and a new [workbookComment](../resources/workbookcomment.md) object in the response body.

## Examples

### Request

The following is an example of the request.
<!-- {
  "blockType": "request",
  "name": "create_workbookcomment_from_workbook"
}-->

```http
POST https://graph.microsoft.com/beta/drive/root/workbook/comments
Content-type: application/json

{
  "content": "This is text of posting comment",
  "contentType": "plain"
}
```

### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability. All the properties will be returned from an actual call.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.workbookComment"
} -->

```http
HTTP/1.1 201 Created
Content-type: application/json

{
  "content": "This is text of posting comment",
  "contentType": "plain"
  "id": "{F603CBAC-7F1C-4110-BECB-D9AEF9B9BFED}"
}
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "Create workbookComment",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->
