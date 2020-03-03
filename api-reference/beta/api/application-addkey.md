---
title: "application: addKey"
description: "Add a key credential to an application."
localization_priority: Normal
author: "davidmu1"
ms.prod: "microsoft-identity-platform"
doc_type: "apiPageType"
---

# application: addKey

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Add a key credential to an [application](../resources/application.md). This method, along with [removeKey](application-removekey.md), can be used by an application to automate rolling its expiring keys.

> [!Note]
> [Create application](../api/application-post-applications.md) and
[Update application](../api/application-update.md) operations can continue to be used to add and update key credentials for any application with or without a user's context.

As part of the request validation for this method, a proof of possession of an existing key is verified before the action can be performed. 

Applications that don’t have any existing valid certificates (no certificates have been added yet, or all certificates have expired), won’t be able to use this service action. You can use the [Update application](../api/application-update.md) operation to perform an update instead.

## Permissions

None. An application does not need any specific permission to roll its own keys.

## HTTP request

<!-- { "blockType": "ignored" } -->

```http
POST /applications/{id}/addKey
```

## Request headers

| Name           | Description                |
|:---------------|:---------------------------|
| Authorization  | Bearer {token}. Required.  |
| Content-Type   | application/json. Required.|

## Request body

In the request body, provide the following required properties.

| Property	   | Type	|Description|
|:---------------|:--------|:----------|
| keyCredential | [keyCredential](../resources/keycredential.md) | The new application key credential to add. The __type__, __usage__ and __key__ are required properties for this usage. Supported key types are:<br><ul><li>`AsymmetricX509Cert`: The usage must be `Verify`.</li><li>`X509CertAndPassword`: The usage must be `Sign`</li></ul>|
| passwordCredential | [passwordCredential](../resources/passwordcredential.md) | Only __secretText__ is required to be set which should contain the password for the key. This property is required only for keys of type `X509CertAndPassword`. Set it to `null` otherwise.|
| proof | String | A self-signed JWT token used as a proof of possession of the existing keys. This JWT token must be signed using the private key of one of the application's existing valid certificates. The token should contain the following claims:<ul><li>`aud` - Audience needs to be `00000002-0000-0000-c000-000000000000`.</li><li>`iss` - Issuer needs to be the __id__  of the application that is making the call.</li><li>`nbf` - Not before time.</li><li>`exp` - Expiration time should be "nbf" + 10 mins.</li></ul><br>A code [sample](#sample-to-generate-proof-token) to generate this proof of possession token is provided at the end of this topic.|

## Response

If successful, this method returns a `200 OK` response code and a new [keyCredential](../resources/keycredential.md) object in the response body.

## Examples

### Example 1: Add a new key credential to an application

#### Request

The following is an example of the request.

<!-- {
  "blockType": "request",
  "name": "application_addkey"
}-->

```http
POST https://graph.microsoft.com/beta/applications/{id}/addKey
Content-type: application/json

{
    "keyCredential": {
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "key": "MIIDYDCCAki..."
    },
    "passwordCredential": null,
    "proof":"eyJ0eXAiOiJ..."
}
```

#### Response

The following is an example of the response.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "microsoft.graph.keyCredential"
} -->

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#microsoft.graph.keyCredential"
}
```

### Example 2: Add a key credential and an associated password for the key

#### Request

The following is an example of the request.

<!-- {
  "blockType": "request",
  "name": "application_addkey"
}-->

```http
POST https://graph.microsoft.com/beta/applications/{id}/addKey
Content-type: application/json

{
    "keyCredential": {
        "type": "X509CertAndPassword",
        "usage": "Sign",
        "key": "MIIDYDCCAki..."
    },
    "passwordCredential": {
        "secretText": "MKTr0w1..."
    },
    "proof":"eyJ0eXAiOiJ..."
}
```

#### Response

The following is an example of the response.

<!-- {
  "blockType": "response",
  "truncated": true
} -->

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#microsoft.graph.keyCredential"
}
```

<!-- uuid: 16cd6b66-4b1a-43a1-adaf-3a886856ed98
2019-02-04 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "application: addKey",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->

## Sample to generate proof token

The following sample could be used to generate the proof token:

```csharp
using System;
using System.Collections.Generic;
using System.Security.Cryptography.X509Certificates;
using Microsoft.IdentityModel.Tokens;
using Microsoft.IdentityModel.JsonWebTokens;

namespace MicrosoftIdentityPlatformProofTokenGenerator
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the following
            string pfxFilePath = "<Path to your certificate file";
            string password = "<Certificate password>";
            string objectId = "<id of the application object>";

            // Get signing certificate
            X509Certificate2 signingCert = new X509Certificate2(pfxFilePath, password);

            // audience
            string aud = $"00000002-0000-0000-c000-000000000000";

            // aud and iss are the only required claims.
            var claims = new Dictionary<string, object>()
            {
                { "aud", aud },
                { "iss", objectId }
            };

            // token validity should not be more than 10 minutes
            var now = DateTime.UtcNow;
            var securityTokenDescriptor = new SecurityTokenDescriptor
            {
                Claims = claims,
                NotBefore = now,
                Expires = now.AddMinutes(10),
                SigningCredentials = new X509SigningCredentials(signingCert)
            };

            var handler = new JsonWebTokenHandler();
            var x = handler.CreateToken(securityTokenDescriptor);
            Console.WriteLine(x);
        }
    }
}
```
