---
title: Update printer
description: Update the properties of a printer object.
author: nilakhan
localization_priority: Normal
ms.prod: cloud-printing
doc_type: apiPageType
---

# Update printer
Namespace: microsoft.graph

Update the properties of a [printer](../resources/printer.md) object.

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

In addition to the following permissions, the user's tenant must have an active Universal Print subscription. The signed in user must be a [Printer Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#printer-administrator).

>**Note:** Only the app that registered the printer is allowed to update the printer using application permissions.

|Permission type | Permissions (from least to most privileged) |
|:---------------|:--------------------------------------------|
|Delegated (work or school account)| Printer.ReadWrite.All, Printer.FullControl.All |
|Delegated (personal Microsoft account)|Not Supported.|
|Application| Printer.ReadWrite.All |

>**Note:** Right now, only printers that don't have physical device can be updated using application permissions.

## HTTP request

<!-- {
  "blockType": "ignored"
}
-->
``` http
PATCH /print/printers/{printerId}
```

## Request headers
|Name|Description|
|:---|:---|
|Authorization|Bearer {token}. Required.|
|Content-Type|application/json. Required.|

## Request body

### Delegated permissions and JSON payload

If using delegated permissions, in the request body, supply the values for the relevant [printer](../resources/printer.md) fields that should be updated. Existing properties that are not included in the request body will maintain their previous values or be recalculated based on changes to other property values. For best performance, don't include existing values that haven't changed. 

The following properties can be updated using delegated permissions.

| Property     | Type        | Description |
|:-------------|:------------|:------------|
|defaults|[printerDefaults](../resources/printerdefaults.md)|The printer's default print settings.|
|location|[printerLocation](../resources/printerlocation.md)|The physical and/or organizational location of the printer.|
|displayName|String|The name of the printer.|

### Application permissions and JSON payload
In the request body, supply the values for the relevant [printer](../resources/printer.md) fields that should be updated. Existing properties that are not included in the request body will maintain their previous values or be recalculated based on changes to other property values. For best performance, don't include existing values that haven't changed. 

The following properties can be updated using application permissions.

| Property     | Type        | Description |
|:-------------|:------------|:------------|
|defaults|[printerDefaults](../resources/printerdefaults.md)|The printer's default print settings.|
|capabilities|[printerCapabilities](../resources/printerCapabilities.md)|The capabilities of the printer associated with this printer share.|
|displayName|String|The name of the printer.|
|manufacturer|String|The manufacturer of the printer.|
|model|String|The model name of the printer.|
|status|[printerStatus](../resources/printerstatus.md)|The processing status of the printer, including any errors.|
|isAcceptingJobs|Boolean|Whether the printer is currently accepting new print jobs.|

### Application permissions and IPP payload

With application permissions, a printer can also be updated using an Internet Printing Protocol (IPP) payload. In this case, the request body contains a binary stream that represents the Printer Attributes group in [IPP encoding](https://tools.ietf.org/html/rfc8010).

The client MUST supply a set of Printer attributes with one or more values (including explicitly allowed out-of-band values) as defined in [RFC8011 section 5.2](https://tools.ietf.org/html/rfc8011#section-5.2) Job Template Attributes ("xxx-default", "xxx-supported", and "xxx-ready" attributes), [Section 5.4](https://tools.ietf.org/html/rfc8011#section-5.4) Printer Description Attributes, and any attribute extensions supported by the Printer. The value(s) of each Printer attribute
supplied replaces the value(s) of the corresponding Printer attribute on the target Printer object. For attributes that can have multiple values (1setOf), all values supplied by the client replace all values of the corresponding Printer object attribute.

## Response

### Delegated permissions and JSON payload

If using delegated permissions, if successful, this method returns a `200 OK` response code and an updated [printer](../resources/printer.md) object in the response body.

### Application permissions and JSON payload

If using delegated permissions, if successful, this method returns a `200 OK` response code and an updated [printer](../resources/printer.md) object in the response body.

### Application permissions and IPP payload

If using application permissions, if successful, this method returns `204 No content` response code. It does not return anything in the response body.

## Examples

### Request
<!-- {
  "blockType": "request",
  "name": "update_printer"
}
-->
``` http
PATCH https://graph.microsoft.com/v1.0/print/printers/{printerId}
Content-Type: application/json
Content-length: 581

{
  "@odata.type": "#microsoft.graph.printer",
  "defaults": {
    "@odata.type": "microsoft.graph.printerDefaults"
  },
  "location": {
    "@odata.type": "microsoft.graph.printerLocation"
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
  "@odata.type": "#microsoft.graph.printer",
  "id": "5b94422c-422c-5b94-2c42-945b2c42945b",
  "displayName": "String",
  "manufacturer": "String",
  "model": "String",
  "isAcceptingJobs": "Boolean",
  "defaults": {
    "@odata.type": "microsoft.graph.printerDefaults"
  },
  "location": {
    "@odata.type": "microsoft.graph.printerLocation"
  },
  "status": {
    "@odata.type": "microsoft.graph.printerStatus"
  },
  "registeredDateTime": "String (timestamp)",
  "isShared": "Boolean",
  "hasPhysicalDevice": "Boolean"
}
```

