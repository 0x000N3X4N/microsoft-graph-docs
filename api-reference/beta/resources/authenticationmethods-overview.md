---
title: "authentication methods API overview"
description: "Authentication methods are how users authenticate in Azure AD."
localization_priority: Normal
author: "mmcla"
ms.prod: "microsoft-identity-platform"
doc_type: "conceptualPageType"
---

# Azure AD authentication methods overview

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

[Authentication methods](https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-authentication-methods) are the ways that users authenticate in Azure Active Directory (AD). Authentication methods in Azure AD include password and phone (i.e. SMS and voice calls), which are manageable in Microsoft Graph today, among many others such as FIDO2 security keys and the Microsoft Authenticator app. Authentication methods are used in primary, second-factor, and step-up authentication, and also in the self-service password reset (SSPR) process.

These APIs are used to manage a user's authentication methods. 

Some examples:

* You can add a phone number to a user. The user can then use that phone number for SMS and voice call authentication if they're enabled to use in by policy. 
* You can then update that number, or delete it from the user.
* You can enable or disable the number for SMS sign-in.
* You can reset a user's password.

## What authentication methods can be managed in Graph?

|Authentication method       | Description |Examples     |
|:---------------------------|:------------|:------------|
|[passwordAuthenticationMethod](passwordauthenticationmethod.md)| A password is currently the default primary authentication method in Azure AD.|Reset a user's password|
|[phoneAuthenticationMethod](phoneauthenticationmethod.md)|A phone can be used by a user to authenticate using [SMS or voice calls](https://docs.microsoft.com/en-us/azure/active-directory/authentication/concept-authentication-methods#phone-options) (as allowed by policy).|See a user's authentication phone numbers. Add, update, or remove a phone number to a user. Enable or disable a primary mobile phone for SMS sign-in.|

## Next steps

* Review the authentication method types listed above and their various methods.
* Try the API in the [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
