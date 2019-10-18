---
title: "Set up change notifications that include resource data (preview)"
description: "Microsoft Graph uses a webhook mechanism to deliver change notifications to clients. Notifications can include resource properties."
author: "piotrci"
localization_priority: Priority
---

# Set up change notifications that include resource data (preview)

Microsoft Graph allows apps to subscribe to change notifications for resources via [webhooks](webhooks.md). You can now set up subscriptions to resource data (such as the content of a Microsoft Teams chat message) to be included in notifications. Your app can then run its business logic without the need to make additional API calls to fetch the changing resource. As a result, the app makes fewer API calls and has better performance, which is beneficial in large scale scenarios.

Requesting resource data in notifications requires you to implement the following additional logic to satisfy data access and security requirements: 

- [Handle](#subscription-lifecycle-notifications) special subscription lifecycle notifications - `reauthorizationRequired` - to maintain an uninterrupted flow of data.
- [Validate](#validating-the-authenticity-of-notifications) the authenticity of notifications as having originated from Microsoft Graph.
- [Provide](#decrypting-resource-data-from-change-notifications) a public encryption key and use a private key to decrypt resource data received through notifications.

## Resource data in notification payload

In general, this type of change notifications include the following resource data in the payload:

- ID and type of the resource instance, returned in the **resourceData** property.
- All the property values of that resource instance, encrypted as specified in the subscription, returned in the **encryptedContent** property.
- Or, depending on the resource, specific properties returned in the **resourceData** property. To get only specific properties, specify them as part of the **resource** URL in the subscription, using a `$select` parameter.  


## Supported resources

The following resources support change notifications that include resource data:

- Chat messages (preview)
  - New or changed messages in a specific Teams channel: `/teams/{id}/channels/{id}/messages`
  - New or changed messages in a specific Teams chat: `/chats/{id}/messages`

This article walks through the details, using the **chatMessage** resource as an example.

## Creating a subscription

To have resource data included in change notifications, you **must** specify the following properties, in addition to those that are usually specified when creating a [subscription](webhooks.md):

- **includeResourceData** set to `true` to explicitly request resource data.
- An optional `$select` operator in the resource path to select the properties to be included.
- **lifecycleNotificationUrl** - an endpoint to which where [lifecycle notifications](#subscription-lifecycle-notifications) will be delivered. This can be the same or different as **notificationUrl**.
- **encryptionCertificate** containing only the public key that Microsoft Graph will use to encrypt resource data. You will keep the corresponding private key which will be used to [decrypt the content](#decrypting-resource-data-from-change-notifications).
- **encryptionCertificateId** your own identifier for the certificate. It will be included in notifications so you can identify which certificate to use for decryption.

### Subscription request example

The following example subscribes to resource changes - channel messages being created or updated in Microsoft Teams. It also subscribes to life cycle events that can affect the flow of change notifications; find more details on life cycle notifications in the next section.

```http
POST https://graph.microsoft.com/beta/subscriptions
Content-Type: application/json
{
  "changeType": "created,updated",
  "notificationUrl": "https://webhook.azurewebsites.net/api/resourceNotifications",
  "lifecycleNotificationUrl": "https://webhook.azurewebsites.net/api/lifecycleNotifications",
  "resource": "/teams/{id}/channels/{id}/messages",
  "includeResourceData": true,
  "encryptionCertificate": "{base64encodedCertificate}",
  "encryptionCertificateId": "{customId}",
  "expirationDateTime": "2019-09-19T11:00:00.0000000Z",
  "clientState": "{secretClientState}"
}
```

### Subscription response
```http
POST https://graph.microsoft.com/beta/subscriptions
Content-Type: application/json
{
  "changeType": "created,updated",
  "notificationUrl": "https://webhook.azurewebsites.net/api/resourceNotifications",
  "lifecycleNotificationUrl": "https://webhook.azurewebsites.net/api/lifecycleNotifications",
  "resource": "/teams/{id}/channels/{id}/messages",
  "includeResourceData": true,
  "encryptionCertificateId": "{customId}",   
  "encryptionCertificateThumbprint": "{thumbprintFromTheCertificate}",
  "expirationDateTime": "2019-09-19T11:00:00.0000000Z",
  "clientState": "{secretClientState}"
}
```

> **Note:** 
> - Use the same hostname for both notifications URLs.
> - You need to validate both notification endpoints as described in [here](webhooks.md#managing-subscriptions). If you choose to use the same URL for both endpoints you will receive and respond to two validation requests.
> - You cannot update (`PATCH`) the existing subscriptions to add the **lifecycleNotificationUrl** property. You should remove such existing subscriptions, and create new subscriptions and specify the **lifecycleNotificationUrl** property.

## Subscription lifecycle notifications

Subscription lifecycle notifications inform you about actions you need to take in order to maintain an uninterrupted flow of notifications. Unlike resource change notifications, which inform about an instance of a resource changing, these notifications tell you about the subscription itself, and its current state in the lifecycle.

These notifications will be delivered to the **lifecycleNotificationUrl**. You should identify the type of notification, and take the corresponding action to ensure that the change notifications continue to flow.

### Re-authorization challenges

When the **lifecycleEvent** property in a notification indicates `reauthorizationRequired`, you must re-authorize the subscription to maintain the data flow.

When you create a long-lived subscription (for example, one that lasts for 3 days), resource data notifications flows to the location indicated in **notificationUrl**. However, at any point in time, Microsoft Graph may require that you re-authorize the subscription to prove that you still have access to resource data, in case the conditions of access have changed since the subscription was created. The following are examples of changes that affect your access to data:

- A tenant admin may revoke your app's permissions to read the resource
- The user who provides the authentication token to your app (interactive scenarios) may be subject to dynamic policies based on factors including their location, device state, or risk assesment. For example, if the user changes their physical location, they may no longer be allowed to access the data, and your app will not be able to re-authorize the subscription. For more information on dynamic policies that control access, see [Azure AD conditional access policies](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/overview). 

Given an active, non-expired subscription, the flow looks as follows:

1. Microsoft Graph decides that a subscription requires re-authorization to maintain the resource notification flow.
    1. The reasons for this may vary from resource to resource, and may change over time. You do not need to understand the specific cases in which re-authorization events occur, you only need to respond to them.

2. Microsoft Graph sends an authorization challenge notification to the **lifecycleNotificationUrl**
    1. Note that the flow of resource notifications may continue for a while, giving you extra time to respond. However, eventually resource notification delivery will be paused, until you take the required action.

3. You can respond to this notification in two ways:
    1. Re-authorize the subscription; this does not extend the subscription's expiry date.
    2. Renew the subscription; this both re-authorizes and extends the expiry date.

  Note: both actions require you to present a valid authentication token; same as when creating or renewing a subscription.

4. If you successfully re-authorize or renew the subscription, resource notifications will continue. Otherwise, resource notifications will remain paused.
    
#### reauthorizationRequired notification example

```json
{
  "value": [
    {
      "lifecycleEvent": "reauthorizationRequired",
      "subscriptionId": "e3898f08-5cd0-4a6a-80fc-6addbfb73b7b",
      "subscriptionExpirationDateTime": "2019-09-18T00:52:45.9696658+00:00",
      "clientState": "<secretClientState>",
      "tenantId": "84bd8158-6d4d-4958-8b9f-9d6445542f95"
    }
  ]
}
```

A few things to note about this type of notification:
- The `"lifecycleEvent": "reauthorizationRequired"` field designates this notification as an authorization challenge.
- The notification does not contain any information about a specific resource, because it is not related to a resource change, but to the subscription state change.
- Similar to resource notifications, lifecycle notifications may be batched together (in the **value** array), each with a possibly different **lifecycleEvent** value. Process each notification in the batch accordingly.

#### Actions to take

1. [Acknowledge](webhooks.md#notifications) the receipt of the notification, by responding to the POST call with `202 - Accepted`.
2. [Validate](webhooks.md#notifications) the authenticity of the notification.
3. Ensure the app has a valid access token to take the next step. 
> **Note:** If you are using one of the [authentication libraries](https://docs.microsoft.com/azure/active-directory/develop/reference-v2-libraries) they will handle this for you by either reusing a valid cached token, or obtaining a new token, including asking the user to login again (e.g. with a new password). Note that obtaining a new token may fail, since the conditions of access may have changed, and the caller may no longer be allowed access to the resource data.

4. Call either of these two APIs - if successful, both will have the affect of resuming the resource notification flow.
    1. To re-authorize the subscription, without extending its expiration date, call the `/reauthorize` action:
```http
POST  https://graph.microsoft.com/beta/subscriptions/{id}/reauthorize
Content-type: application/json
```
  2. To re-authorize and renew the subscription at the same time, perform a regular renew action:
```http
PATCH https://graph.microsoft.com/beta/subscriptions/{id}
Content-Type: application/json

{
  "expirationDateTime": "2019-09-21T11:00:00.0000000Z",
}
```

> **Note:** This action may fail, because the authorization checks performed by the system may deny the app or the user access to the resource. It may be necessary for the app to obtain a new access token from the user to successfully reauthorize a subscription. You may retry these actions later, at any time, for example when the conditions of access have changed. Any resource changes in the time period from when the lifecycle notification was sent, to when the app re-creates the subscription successfully, will be lost. The app will need to fetch those changes on its own.

#### Implementation guidelines

Keep the following things in mind:

1. Authorization challenges do not replace the need for you to renew your subscriptions before they expire. While you can choose to renew subscriptions as a response to challenges, the challenges may not be generated by the system for all of your subscriptions. For example, subscriptions that do not have any activity - no resource notifications pending delivery - may not signal any re-authorization challenges to your app. Continue to renew your subscriptions, as described [here](webhooks.md#managing-subscriptions).

2. Do not make assumptions about the frequency at which you may see challenges for your subscriptions, it is subject to change. The main reason for these signals is for you, the app developer, not to have to know all the cases in which re-authorization of your subscription is required; instead, Microsoft Graph tells you when you need to take action. Your app should be ready to handle these challenges anywhere from once every few minutes per each subscription to very rarely, only for some subscriptions.

### Future-proof your code

In the future Microsoft Graph will add more types of subscription lifecycle notifications. They will be posted to the same endpoint: **lifecycleNotificationUrl**, but they will have a different value under **lifecycleEvent** and may contain a slightly different schema and properties, specific to the scenario for which they will be issued.

You should implement your code in a future-proof way so it does not break when Microsoft Graph introduces new types of lifecycle notifications. We recommend the following approach:

1. Explicitly identify each notification as an event that you support, using the **lifecycleEvent** property. For example, look for the `"lifecycleEvent": "reauthorizationRequired"` property to identify a specific event, and handle it.

1. In your app, ignore any lifecycle events that the app does not recognize, and log them to gain awareness.

1. Watch for announcements of notifications for new scenarios, as there may be more types of lifecycle notifications in the future.

1. At your discretion, look up the related documentation for new lifecycle notifications and implement support for them as appropriate.

## Validating the authenticity of notifications

When you receive notifications with resource data you will likely execute some business logic based on that data. It is important that you first verify the authenticity of each notification; otherwise a 3rd party could spoof your app with false notifications and make it execute its business logic incorrectly, which could result in a security incident.

For basic notifications, which do not contain resource data, this validation can be simplified and based on the **clientState** value, as described [here](webhooks.md#notifications). That is acceptable, because you rely on additional trusted Microsoft Graph calls to get access to resource data, and therefore the impact of any spoofing attempts is limited. A more thorough validation is recommended before you process resource data delivered via notifications.

### Validation tokens in the notification

A notification contains an additional property - **validationTokens** - containing an array of JWT tokens generated by Microsoft Graph; there will be a single token for each distinct app and tenant pair for whom there is an item in the **value** array. Keep in mind that notifications may contain a mix of items for various apps and tenants that subscribed using the same **notificationUrl**.

In this example, the notification contains two items for the same app, and for two different tenants, therefore the **validationTokens** array contains two tokens that need to be validated.

```json
{
	"value": [
		  {
			"subscriptionId": "76619225-ff6b-4489-96ca-4ef547e78b22",
      "tenantId": "84bd8158-6d4d-4958-8b9f-9d6445542f95",
			"changeType": "created",
			...
		  },
      {
			"subscriptionId": "e990d58f-fd93-40af-acf7-a7c907c5d8ea",
      "tenantId": "46d9e3bd-6309-4177-a016-b256a411e30f",
			"changeType": "created",
			...
			}
	],
	"validationTokens": [
		"eyJ0eXAiOiJKV1QiLCJhb...",
    "cGlkYWNyIjoiMiIsImlkc..."
	]
}
```
### How to validate

If you are new to token validation, this [blog article](http://www.cloudidentity.com/blog/2014/03/03/principles-of-token-validation/) contains a useful overview. We recommend that you use an SDK, such as Microsoft's [System.IdentityModel.Tokens.Jwt](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/) library for .NET, or a 3rd party library for a different platform.

> **Note:** Make sure to always send a `202 - Accepted` status code in in the response to the notification; do that before validating the notification (e.g. if you store notifications in queues for later processing) or after (if you process them on the fly) - even if validation failed. Accepting a notification prevents unnecessary delivery retries and it also prevents any potential rogue actors from finding out if they passed or failed validation. You can always choose to ignore an invalid notification after you have accepted it.

1. Validate that the token has not expired.

2. Validate the token has not been tampered with and was issued by the expected authority - Microsoft Azure Active Directory. You should not accept tokens issued by any other authority.
  - Obtain the signing keys from the common configuration endpoint: `https://login.microsoftonline.com/common/.well-known/openid-configuration`. This configuration should be cached by your app for a period of time; however note that the configuration is updated frequently as signing keys are rotated daily.
  - Verify the signature of the JWT token using those keys.

3. Validate that the token was issued for your app that is subscribing to change notifications.
  - Validate the "audience" in the token matches your app id.
  - If you have more than one app receiving notifications, make sure to check for multiple ids

> **Note:** The above steps are part of standard validation logic in JWT token libraries and can typically be executed as a singlee function call. 

4. **Critical**: Validate that the app that generated the token represents the Microsoft Graph change notification publisher. This ensures that notifications are not sent by a different app that is not Microsoft Graph
  - Check that the **appid** property in the token matches the expected value of `0bf30f3b-4a52-48df-9a82-234910c4a086`.

This validation should be performed on every JWT token in the **validationTokens** array. If any tokens fail, you should consider the notification suspicious and investigate further.

#### Sample JWT token

Here is an example of the properties included in the JWT token that are needed for validation:

```json
{
  "aud": "8e460676-ae3f-4b1e-8790-ee0fb5d6148f",                            <-- this should be your app's id
  "iss": "https://sts.windows.net/84bd8158-6d4d-4958-8b9f-9d6445542f95/",
  "iat": 1565046813,
  "nbf": 1565046813,
  "exp": 1565075913,                                                        <--  expiration date
  "aio": "42FgYKhZ+uOZrHa7p+7tfruauq1HAA==",
  "appid": "0bf30f3b-4a52-48df-9a82-234910c4a086",                          <-- this represents the notification publisher and must always be the same value of 0bf30f3b-4a52-48df-9a82-234910c4a086
  "appidacr": "2",
  "idp": "https://sts.windows.net/84bd8158-6d4d-4958-8b9f-9d6445542f95/",
  "tid": "84bd8158-6d4d-4958-8b9f-9d6445542f95",
  "uti": "-KoJHevhgEGnN4kwuixpAA",
  "ver": "1.0"
}
```

## Decrypting resource data from change notifications

The data included in the **resourceData** property of the notification is limited to only the basic id and type information about the resource. The **encryptedData** property contains the full resource data that was encrypted by Microsoft Graph using the public key provided by you; it also contains additional values required for verification and decryption. This is done to increase the security of customer data accessed via notifications. It is your responsibility to secure the private key to ensure that customer data cannot be decrypted by a 3rd party, even if they managed to intercept the original notifications.

### Managing encryption keys

1. You need to obtain a certificate with a pair of assymetric keys. The certificate can be self-signed - Microsoft Graph does not verify the certificate issuer, but only uses the public key for encryption. We recommend [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis) as the solution to create, rotate and securily manage certificates.
  - the key must be of type `RSA`
  - the key size must be between 2048 and 4096 bits

2. Export the certificate **ensuring that only the public key** is included. The certificate must be exported as a Base64-encoded X.509 certificate.

3. When creating the subscription:
  - Provide the certificate in the **encryptionCertificate** property; use the Base64-encoded content the certificate was exported in.
  - Provide your own identifier in the **encryptionCertificateId**. It will allow you to match your certificates to the notifications you receive and can also be used to retrieve certificates from your certificate store. The length of this id can be up to 128 characters.

4. The private key must be securily held and managed by you. Your notification processing code will need to have access to the private key to decrypt resource data.

#### Rotating keys

It is a recommmended practice to periodically change your assymetric keys to minimize the risk of a private key becoming compromised. If you want to introduce a new pair of keys, follow these steps:

1. Obtain a new certificate with a new pair of assymetric keys. Use it for all new subscriptions being created.

2. Update existing subscriptions with the new certificate key; you can do this as part of regular subscription renewal or enumerate all subscriptions and provide the key. The certificate can be updated by providing the **encryptionCertificate** and **encryptionCertificateId** properties in the `PATCH` operation on the subscription.

3. Some things to keep in mind:
    - For a period of time the old certificate may still be used for encryption. Your app must have access to both old and new certificates to be able to decrypt content.
    - Use the **encryptionCertificateId** property in each notification to  identify the correct key to use.
    - Discard of the old certificate only when you have seen no recent notifications referencing it.

### How to decrypt

To optimize performance, Microsoft Graph uses a two-step encryption process:
  - It generates a single use symmetric key, and uses it to encrypt resource data.
  - It uses the public assymetric key - provided by you - to encrypt the symmetric key and includes it in the notification.

To decrypt resource data, your app should perform the reverse steps, using the properties under **encryptedContent** in each notification item:

1. Use the **encryptionCertificateId** property to identify the certificate that should be used.

2. Initialize an RSA cryptographic component (such as the .NET [RSACryptoServiceProvider](https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.rsacryptoserviceprovider.decrypt?view=netframework-4.8)) with the private key.

3. Use it to decrypt the symmetric key delivered in the **dataKey** property of each item in the notification.
  - Note: the decryption algorithm should use the OAEP padding.

4. Use the symmetric key to calculate the HMAC-SHA256 signature of the value in **data**.
  - Compare it to the value in **dataSignature**. If they do not match, assume the payload has been tampered with and do not decrypt it.

5. Use the symmetric key with an AES cryptographic component (such as the .NET [AesCryptoServiceProvider](https://docs.microsoft.com/en-us/dotnet/api/system.security.cryptography.aescryptoserviceprovider?view=netframework-4.8)) to decrypt the content in **data**.
The decryption parameters for the AES algorithm are as follows:
  - Padding: PKCS7
  - Cipher mode: CBC
  - The "initialization vector" must be set by copying the first 16 bytes of the symmetric key used for decryption.

6. The decrypted value is a string json representation of the resource included in the notification.

> **Note:** always assume that the symmetric key is different for each item in the notification.

#### Sample notification with encrypted resource data

```json
{
	"value": [
		{
			"subscriptionId": "76222963-cc7b-42d2-882d-8aaa69cb2ba3",
			"changeType": "created",
			...
			"resource": "teams('d29828b8-c04d-4e2a-b2f6-07da6982f0f0')/channels('19:f127a8c55ad949d1a238464d22f0f99e@thread.skype')/messages('1565045424600')/replies('1565047490246')",
			"resourceData": {
				"id": "1565293727947",
				"@odata.type": "#Microsoft.Graph.ChatMessage",
				"@odata.id": "teams('88cbc8fc-164b-44f0-b6a6-b59b4a1559d3')/channels('19:8d9da062ec7647d4bb1976126e788b47@thread.tacv2')/messages('1565293727947')/replies('1565293727947')"
			},
			"encryptedContent": {
				"data": "<encryptedDataThatProducesAFullResource>",
        "dataSignature": "<HMAC-SHA256 hash>",
				"dataKey": "<encryptedSymmetricKeyFromGraph>",
				"encryptionCertificateId": "MySelfSignedCert/DDC9651A-D7BC-4D74-86BC-A8923584B0AB",
				"encryptionCertificateThumbprint": "07293748CC064953A3052FB978C735FB89E61C3D",
			}
		}
	],
	"validationTokens": [
		"eyJ0eXAiOiJKV1QiLCJhbGciOiJSU..."
	]
}
```

#### Code sample using C# .NET

These are some useful code snippets using C# and .NET for each stage of decryption.

#### Decryption of the symmetric key

```csharp
// initialize with the private key matching the encryptionCertificateId
RSACryptoServiceProvider rsaProvider = ...;        
byte[] encryptedSymmetricKey = Convert.FromBase64String(<value from dataKey property>);

// decrypt using OAEP padding
byte[] decryptedSymmetricKey = rsaProvider.Decrypt(encryptedSymmetricKey, fOAEP: true);

// decryptedSymmetricKey can now be used with the AES algorithm
```

### Comparing data signature using HMAC-SHA256

```csharp
byte[] decryptedSymmetricKey = <the aes key decrypted in the previous step>;
byte[] encryptedPayload = <the value from the data property, still encrypted>;
byte[] expectedSignature = <the value from the dataSignature property>;
byte[] actualSignature;

using (HMACSHA256 hmac = new HMACSHA256(decryptedSymmetricKey))
{
    actualSignature = hmac.ComputeHash(encryptedPayload);
}
if (actualSignature.SequenceEqual(expectedSignature))
{
    // continue with decryption of the encryptedPayload
}
else
{
    // do not attempt to decrypt encryptedPayload. assume notification payload has been tampered with and investigate 
}
```

#### Decryption of the resource data content

```csharp
AesCryptoServiceProvider aesProvider = new AesCryptoServiceProvider();
aesProvider.Key = decryptedSymmetricKey;
aesProvider.Padding = PaddingMode.PKCS7;
aesProvider.Mode = CipherMode.CBC;

// obtain the intialization vector from the symmetric key itself
int vectorSize = 16;
byte[] iv = new byte[vectorSize];
Array.Copy(decryptedSymmetricKey, iv, vectorSize);
aesProvider.IV = iv;

byte[] encryptedPayload = Convert.FromBase64String(<value from dataKey property>);

string decryptedResourceData;
// decrypt the resource data content
using (var decryptor = aesProvider.CreateDecryptor())
{
  using (MemoryStream msDecrypt = new MemoryStream(encryptedPayload))
  {
      using (CryptoStream csDecrypt = new CryptoStream(msDecrypt, decryptor, CryptoStreamMode.Read))
      {
          using (StreamReader srDecrypt = new StreamReader(csDecrypt))
          {
              decryptedResourceData = srDecrypt.ReadToEnd();
          }
      }
  }
}

// decryptedResourceData now contains a string json representing the resource
```

## See also

- [Subscription resource type](/graph/api/resources/subscription?view=graph-rest-beta)
- [Get subscription](/graph/api/subscription-get?view=graph-rest-1.0)
- [Create subscription](/graph/api/subscription-post-subscriptions?view=graph-rest-1.0)
