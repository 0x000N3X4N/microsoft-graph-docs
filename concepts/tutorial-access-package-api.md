---
title: "Tutorial: Create an access package using Microsoft Graph APIs"
description: "Learn how to create an access package and request access to it using Microsoft Graph APIs."
author: "davidmu1"
localization_priority: Normal
ms.prod: "microsoft-identity-platform"
---

# Tutorial: Create an access package using Microsoft Graph APIs

Managing access to all the resources employees need, such as groups, applications, and sites, is an important function for organizations. You want to grant employees the right level of access they need to be productive and remove their access when it is no longer needed. Azure AD entitlement management using Microsoft Graph APIs enables you to manage this type of access.

In this tutorial, you've been asked to develop code to create a package of resources for a marketing campaign that internal users can self-service request. Requests do not require approval and user's access expires after 30 days. For this tutorial, the marketing campaign resources are just membership in a single group, but it could be a collection of groups, applications, or SharePoint Online sites.

The response objects shown in this tutorial may be shortened for readability. All the properties are returned in an actual call.

## Prerequisites

To use Azure AD entitlement management, you must have one of the following licenses:

- Azure AD Premium P2
- Enterprise Mobility + Security (EMS) E5 license

For more information, see [License requirements](https://docs.microsoft.com/azure/active-directory/governance/entitlement-management-overview#license-requirements).

**List of all APIs used in this tutorial**

Make sure you have the corresponding permissions to call the following APIs.

| Resource type | Method |
| ------------- | ------ |
| [user](https://docs.microsoft.com/graph/api/resources/user?view=graph-rest-beta) |  [Create user](https://docs.microsoft.com/graph/api/user-post-users?view=graph-rest-beta)<br>[Delete user](https://docs.microsoft.com/graph/api/user-delete?view=graph-rest-beta) |
| [unifiedRoleDefinition](https://docs.microsoft.com/graph/api/resources/unifiedroledefinition?view=graph-rest-beta) | [List unifiedRoleDefinitions](https://docs.microsoft.com/graph/api/rbacapplication-list-roledefinitions?view=graph-rest-beta) |
| [unifiedRoleAssignment](https://docs.microsoft.com/graph/api/resources/unifiedroleassignment?view=graph-rest-beta) |  [Create unifiedRoleAssignment](https://docs.microsoft.com/graph/api/rbacapplication-post-roleassignments?view=graph-rest-beta) |
| [group](https://docs.microsoft.com/graph/api/resources/group?view=graph-rest-beta) | [Create group](https://docs.microsoft.com/graph/api/group-post-groups?view=graph-rest-beta)<br>[List group members](https://docs.microsoft.com/graph/api/group-list-members?view=graph-rest-beta)<br>[Delete group](https://docs.microsoft.com/graph/api/group-delete?view=graph-rest-beta) |
| [accessPackageCatalog](https://docs.microsoft.com/graph/api/resources/accesspackagecatalog?view=graph-rest-beta) | [List accessPackageCatalogs](https://docs.microsoft.com/graph/api/accesspackagecatalog-list?view=graph-rest-beta)<br>[List accessPackageResources](https://docs.microsoft.com/graph/api/accesspackagecatalog-list-accesspackageresources?view=graph-rest-beta)<br>[List accessPackageResourceRoles](https://docs.microsoft.com/graph/api/accesspackagecatalog-list-accesspackageresourceroles?view=graph-rest-beta) |
| [accessPackageResourceRequest](https://docs.microsoft.com/graph/api/resources/accesspackageresourcerequest?view=graph-rest-beta) | [Create accessPackageResourceRequest](https://docs.microsoft.com/graph/api/accesspackageresourcerequest-post?view=graph-rest-beta)
| [accessPackage](https://docs.microsoft.com/graph/api/resources/accesspackage?view=graph-rest-beta) | [Create accessPackage](https://docs.microsoft.com/graph/api/accesspackage-post?view=graph-rest-beta) |
| [accessPackageResourceRoleScope](https://docs.microsoft.com/graph/api/resources/accesspackageresourcerolescope?view=graph-rest-beta) | [Create accessPackageResourceRoleScope](https://docs.microsoft.com/graph/api/accesspackage-post-accesspackageresourcerolescopes?view=graph-rest-beta) |
| [accessPackageAssignmentPolicy](https://docs.microsoft.com/graph/api/resources/accesspackageassignmentpolicy?view=graph-rest-beta) | [Create accessPackageAssignmentPolicy](https://docs.microsoft.com/graph/api/accesspackageassignmentpolicy-post?view=graph-rest-beta)<br>[List accessPackageAssignmentPolicies](https://docs.microsoft.com/graph/api/accesspackageassignmentpolicy-list?view=graph-rest-beta) |
| [accessPackageAssignmentRequest](https://docs.microsoft.com/graph/api/resources/accesspackageassignmentrequest?view=graph-rest-beta) | [Create accessPackageAssignmentRequest](https://docs.microsoft.com/graph/api/accesspackageassignmentrequest-post?view=graph-rest-beta)<br>[List accessPackageAssignmentRequests](https://docs.microsoft.com/graph/api/accesspackageassignmentrequest-list?view=graph-rest-beta) |

## Step 1: Create user accounts and a group

A resource directory has one or more resources to share. In this step, you create a group named **Marketing resources** in the directory that is the target resource for entitlement management. You also set up an internal requestor.

Sign in to Microsoft Graph Explorer (recommended), Postman, or any other API client you use

1. Start [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).
2. Select **Sign-In with Microsoft** and sign in using an Azure AD global administrator or App Admin credentials.
3. Upon successful sign-in, you'll see the user account details in the left-hand pane.

### Create user accounts

For this tutorial, you create two user accounts. You create an account for administering an access package, and you create an account that is used to request access to the resources in the access package. When you make these calls, change `contoso.onmicrosoft.com` to the address of your tenant. You can find tenant information on the Azure Active Directory overview page. Record the value of the **id** property that is returned to be used later in the tutorial.

#### Request

``` http
POST https://graph.microsoft.com/beta/users
Content-type: application/json

{
  "accountEnabled":true,
  "displayName":"Admin1",
  "mailNickname":"Admin1",
  "userPrincipalName":"Admin1@contoso.onmicrosoft.com",
  "passwordProfile": {
    "forceChangePasswordNextSignIn":true,
    "password":"Contoso1234"
  }
}
```

#### Response

``` http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#users/$entity",
  "id": "792006a5-1d63-4d63-81c7-ec0808181486",
  "deletedDateTime": null,
  "accountEnabled": true,
  "ageGroup": null,
  "businessPhones": [],
  "city": null,
  "createdDateTime": null,
  "creationType": null,
  "companyName": null,
  "consentProvidedForMinor": null,
  "country": null,
  "department": null,
  "displayName": "Admin1",
  "employeeId": null,
  "faxNumber": null,
  "givenName": null,
  "imAddresses": [],
  "infoCatalogs": [],
  "isResourceAccount": null,
  "jobTitle": null,
  "legalAgeGroupClassification": null,
  "mail": null,
  "mailNickname": "Admin1"
}
```

#### Request

``` http
POST https://graph.microsoft.com/beta/users
Content-type: application/json

{
  "accountEnabled":true,
  "displayName":"Requestor1",
  "mailNickname":"Requestor1",
  "userPrincipalName":"Requestor1@contoso.onmicrosoft.com",
  "passwordProfile": {
    "forceChangePasswordNextSignIn":true,
    "password":"Contoso1234"
  }
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#users/$entity",
  "id": "ce02eca8-752b-4ecf-ac29-aa9bccd87606",
  "deletedDateTime": null,
  "accountEnabled": true,
  "ageGroup": null,
  "businessPhones": [],
  "city": null,
  "createdDateTime": null,
  "creationType": null,
  "companyName": null,
  "consentProvidedForMinor": null,
  "country": null,
  "department": null,
  "displayName": "Requestor1",
  "employeeId": null,
  "faxNumber": null,
  "givenName": null,
  "imAddresses": [],
  "infoCatalogs": [],
  "isResourceAccount": null,
  "jobTitle": null,
  "legalAgeGroupClassification": null,
  "mail": null,
  "mailNickname": "Requestor1",
}
```

### Get role definitions

To assign the global administrator privileges to the **Admin1** account, you need to obtain the identifier of the administrator role. In Microsoft Graph, the Global Administrator role is referred to as **Company Administrator**. Record the value of the **id** property that is returned to use later in this tutorial.

#### Request

```http
GET https://graph.microsoft.com/beta/roleManagement/directory/roleDefinitions?$filter=(displayName eq 'Company Administrator')
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleDefinitions",
  "value": [
    {
      "id": "62e90394-69f5-4237-9190-012177145e10",
      "description": "Can manage all aspects of Azure AD and Microsoft services that use Azure AD identities.",
      "displayName": "Company Administrator",
      "isBuiltIn": true,
      "isEnabled": true,
      "resourceScopes": [
        "/"
      ],
      "templateId": "62e90394-69f5-4237-9190-012177145e10",
      "version": "1",
      "rolePermissions": [
        {
          "allowedResourceActions": [],
          "condition": null
        }
      ]
    }
  ]
}
```

### Assign the administrator role

Use the value of the **id** that you obtained from the Company Administrator role definition as the value for the **roleDefinitionId** property. The value of the **principalId** property is the value of the **id** property of the **Admin1** user account that you created.

#### Request

```http
POST https://graph.microsoft.com/beta/roleManagement/directory/roleAssignments
Content-type: application/json

{
  "@odata.type":"#microsoft.graph.unifiedRoleAssignment",
  "roleDefinitionId":"62e90394-69f5-4237-9190-012177145e10",
  "principalId":"792006a5-1d63-4d63-81c7-ec0808181486",
  "directoryScopeId":"/"
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#roleManagement/directory/roleAssignments/$entity",
  "id": "lAPpYvVpN0KRkAEhdxReEKUGIHljHWNNgcfsCAgYFIY-1",
  "principalId": "792006a5-1d63-4d63-81c7-ec0808181486",
  "resourceScope": "/",
  "directoryScopeId": "/",
  "roleDefinitionId": "62e90394-69f5-4237-9190-012177145e10"
}
```

### Create a group

Create a group named **Marketing resources** that is the target resource for entitlement management. Record the value of the **id** property that is returned to use later in this tutorial. 

#### Request

```http
POST https://graph.microsoft.com/beta/groups
Content-type: application/json

{
  "description":"Marketing group",
  "displayName":"Marketing resources",
  "mailEnabled":false,
  "mailNickname":"markres",
  "securityEnabled":true
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#groups/$entity",
  "id": "a468eaea-ed6c-4290-98d2-a96bb1cb4209",
  "deletedDateTime": null,
  "classification": null,
  "createdDateTime": "2020-06-24T16:47:37Z",
  "createdByAppId": "de8bc8b5-d9f9-48b1-a8ad-b748da725064",
  "description": "Marketing group",
  "displayName": "Marketing resources",
  "expirationDateTime": null,
  "groupTypes": [],
  "infoCatalogs": [],
  "isAssignableToRole": null,
  "mail": null,
  "mailEnabled": false,
  "mailNickname": "markres"
}
```

## Step 2: Create an access package

An *access package* is a bundle of resources that a team or project needs and is governed with policies. Access packages are defined in containers called catalogs. In this step, you create a **Marketing Campaign** access package in the General catalog.

### Get the catalog identifier

To add resources to the General catalog, you must first get the identifier of it. Record the value of the **id** property that is returned to use later in this tutorial.

#### Request

```http
GET https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageCatalogs?$filter=(displayName eq 'General')
```

#### Response

```
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageCatalogs",
  "value": [ 
    {
      "id": "ede67938-cda7-4127-a9ca-7c7bf86a19b7",
      "displayName": "General",
      "description": "Built-in catalog.",
      "catalogType": "ServiceDefault",
      "catalogStatus": "Published",
      "isExternallyVisible": true,
      "createdBy": "Azure AD",
      "createdDateTime": "2020-05-30T10:58:05.363Z",
      "modifiedBy": "Azure AD",
      "modifiedDateTime": "2020-05-30T10:58:05.363Z"
    }
  ]
}
```

### Add the group to the catalog

Use the **id** of the General catalog for the value of the **catalogId** property to add the group that you created to it. Provide the **id** of the group that you created for the value of the **originId** property.

#### Request

```http
POST https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageResourceRequests
Content-type: application/json

{
  "catalogId":"ede67938-cda7-4127-a9ca-7c7bf86a19b7",
  "requestType": "AdminAdd",
  "justification": "",
  "accessPackageResource": {
    "displayName": "Marketing resources",
    "description": "Marketing group",
    "url": "https://contoso.sharepoint.com/sites/Marketing",
    "resourceType": "AadGroup",
    "originId": "a468eaea-ed6c-4290-98d2-a96bb1cb4209",
    "originSystem": "AadGroup"
  }
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageResourceRequests/$entity",
  "catalogId": "ede67938-cda7-4127-a9ca-7c7bf86a19b7",
  "executeImmediately": false,
  "id": "2b22d9b0-4c9d-4613-ac59-3debff46f574",
  "requestType": "AdminAdd",
  "requestState": "Delivered",
  "requestStatus": "Fulfilled",
  "isValidationOnly": false,
  "expirationDateTime": null,
  "justification": ""
}
```

### Get catalog resources

In later steps in this tutorial, you need the **id** that was assigned to the group resource in the catalog.

#### Request

```http
GET https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageCatalogs/ede67938-cda7-4127-a9ca-7c7bf86a19b7/accessPackageResources?$filter=(displayName eq 'Marketing resources')
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageResources",
  "value": [
    {
      "id": "e4dd053f-4299-420f-a340-5a17e65d7261",
      "displayName": "Marketing resources",
      "description": "Marketing group",
      "url": "https://account.activedirectory.windowsazure.com/r?tenantId=fa9983b0-d800-4a45-84f6-bc039af82298#/manageMembership?objectType=Group&objectId=a468eaea-ed6c-4290-98d2-a96bb1cb4209",
      "resourceType": "Security Group",
      "originId": "a468eaea-ed6c-4290-98d2-a96bb1cb4209",
      "originSystem": "AadGroup",
      "isPendingOnboarding": false,
      "addedBy": "admin@contoso.onmicrosoft.com",
      "addedOn": "2020-06-26T17:13:23.723Z"
    }
  ]
}
```

### Get resources roles

The group that you added needs to be assigned a role for the access package. Use the **id** of the catalog and the **id** of the group that you recorded to get the **originId** of the Member resource role. Record the value of the **originId** property to use later in this tutorial.

#### Request

```http
GET https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageCatalogs/ede67938-cda7-4127-a9ca-7c7bf86a19b7/accessPackageResourceRoles?$filter=(originSystem+eq+%27AadGroup%27+and+accessPackageResource/id+eq+%27e4dd053f-4299-420f-a340-5a17e65d7261%27+and+displayName+eq+%27Member%27)&$expand=accessPackageResource
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#identityGovernance/entitlementManagement/accessPackageCatalogs('ede67938-cda7-4127-a9ca-7c7bf86a19b7')/accessPackageResourceRoles(accessPackageResource())",
  "value": [
    {
      "id": "00000000-0000-0000-0000-000000000000",
      "displayName": "Member",
      "description": null,
      "originSystem": "AadGroup",
      "originId": "Member_a468eaea-ed6c-4290-98d2-a96bb1cb4209",
      "accessPackageResource@odata.context": "https://graph.microsoft.com/beta/$metadata#identityGovernance/entitlementManagement/accessPackageCatalogs('ede67938-cda7-4127-a9ca-7c7bf86a19b7')/accessPackageResourceRoles('00000000-0000-0000-0000-000000000000')/accessPackageResource/$entity",
      "accessPackageResource": {
        "id": "e4dd053f-4299-420f-a340-5a17e65d7261",
        "displayName": "Marketing resources",
        "description": "Marketing group",
        "url": "https://account.activedirectory.windowsazure.com/r?tenantId=fa9983b0-d800-4a45-84f6-bc039af82298#/manageMembership?objectType=Group&objectId=a468eaea-ed6c-4290-98d2-a96bb1cb4209",
        "resourceType": "Security Group",
        "originId": "a468eaea-ed6c-4290-98d2-a96bb1cb4209",
        "originSystem": "AadGroup",
        "isPendingOnboarding": false,
        "addedBy": "admin@contoso.onmicrosoft.com",
        "addedOn": "2020-06-26T17:13:23.723Z",
        "accessPackageResourceScopes@odata.context": "https://graph.microsoft.com/beta/$metadata#identityGovernance/entitlementManagement/accessPackageCatalogs('ede67938-cda7-4127-a9ca-7c7bf86a19b7')/accessPackageResourceRoles('00000000-0000-0000-0000-000000000000')/accessPackageResource/accessPackageResourceScopes",
        "accessPackageResourceScopes": []
      }
    }
  ]
}
```

### Create the access package

You use the **id** of the General catalog that you recorded earlier to create the access package. Record the **id** of the access package to use later in this tutorial.

#### Request

```http
POST https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackages
Content-type: application/json

{
  "catalogId": "ede67938-cda7-4127-a9ca-7c7bf86a19b7",
  "displayName": "Marketing Campaign",
  "description": "Access to resources for the campaign"
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackages",
  "value": [
    {
      "id": "cf54c6ca-d717-49bc-babe-d140d035dfdd",
      "catalogId": "ede67938-cda7-4127-a9ca-7c7bf86a19b7",
      "displayName": "Sales and Marketing",
      "description": "Access for Sales and Marketing users and guests",
      "isHidden": false,
      "isRoleScopesVisible": false,
      "createdBy": "admin@contoso.onmicrosoft.com",
      "createdDateTime": "2020-05-30T10:58:22.077Z",
      "modifiedBy": "admin@contoso.onmicrosoft.com",
      "modifiedDateTime": "2020-05-30T10:58:22.077Z"
    }
  ]
}
```

### Add a resource role to the access package

Add the Member role to the access package using its **id**. Provide the value of the **originId** for the role that you recorded earlier.

#### Request

```http
POST https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackages/cf54c6ca-d717-49bc-babe-d140d035dfdd/accessPackageResourceRoleScopes
Content-type: application/json

{
  "accessPackageResourceRole":{
    "originId":"Member_a468eaea-ed6c-4290-98d2-a96bb1cb4209",
    "displayName":"Member",
    "originSystem":"AadGroup",
    "accessPackageResource":{"id":"e4dd053f-4299-420f-a340-5a17e65d7261","resourceType":"Security Group","originId":"a468eaea-ed6c-4290-98d2-a96bb1cb4209","originSystem":"AadGroup"}
  },
 "accessPackageResourceScope":{
   "originId":"a468eaea-ed6c-4290-98d2-a96bb1cb4209","originSystem":"AadGroup"
 }
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageResourceRoleScopes/$entity",
  "id": "f2d662bb-89cd-43ad-953e-1f2f6b909279_9173dc27-791a-4d24-a5a3-28f643906e2f",
  "createdBy": "admin@contoso.onmicrosoft.com",
  "createdDateTime": "2020-06-29T19:32:19.3546568Z",
  "modifiedBy": "admin@contoso.onmicrosoft.com",
  "modifiedDateTime": "2020-06-29T19:32:19.3546568Z"
}
```

### Create a direct assignment to the access package

Now that you created the access package and added resources and roles, you can decide who can access it. In the tutorial, you enable the **Requestor1** account that you created to request access to the resources in the access package. For this task, you need these values:
- **id** of the access package for the value of the **accessPackageId** property
- **id** of the **Requestor1** user account for the value of the **id** property in **allowedRequestors**
 
 The value of the **durationInDays** property enables the **Requestor1** account to access the resources in the access package for up to 30 days. Record the value of the **id** property that is returned to use later in this tutorial. 

#### Request

```http
POST https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageAssignmentPolicies
Content-type: application/json

{
  "accessPackageId": "cf54c6ca-d717-49bc-babe-d140d035dfdd",
  "displayName": "direct",
  "description": "direct assignments by administrator",
  "accessReviewSettings": null,
  "durationInDays": 30,
  "requestorSettings": {
    "scopeType": "SpecificDirectorySubjects",
    "acceptRequests": true,
    "allowedRequestors": [
       {
         "@odata.type": "#microsoft.graph.singleUser",
         "isBackup": false,
         "id": "ce02eca8-752b-4ecf-ac29-aa9bccd87606",
         "description": "Requestor1"
       }
    ]
  },
  "requestApprovalSettings": {
    "isApprovalRequired": false,
    "isApprovalRequiredForExtension": false,
    "isRequestorJustificationRequired": false,
    "approvalMode": "NoApproval",
    "approvalStages": []
  }
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageAssignmentPolicies/$entity",
  "id": "6c1f65ec-8c25-4a45-83c2-a1de2a6d0e9f",
  "accessPackageId": "cf54c6ca-d717-49bc-babe-d140d035dfdd",
  "displayName": "direct",
  "description": "direct assignments by administrator",
  "canExtend": false,
  "durationInDays": 30,
  "expirationDateTime": null,
  "createdBy": "admin@contoso.onmicrosoft.com",
  "createdDateTime": "2020-06-29T19:47:44.7399675Z",
  "modifiedBy": "admin@contoso.onmicrosoft.com",
  "modifiedDateTime": "2020-06-29T19:47:44.7555489Z",
  "accessReviewSettings": null,
  "requestorSettings": {
    "scopeType": "SpecificDirectorySubjects",
    "acceptRequests": true,
    "allowedRequestors": [
      {
        "@odata.type": "#microsoft.graph.singleUser",
        "isBackup": false,
        "id": "ce02eca8-752b-4ecf-ac29-aa9bccd87606",
        "description": "Requestor1"
      }
    ]
  },
  "requestApprovalSettings": {
    "isApprovalRequired": false,
    "isApprovalRequiredForExtension": false,
    "isRequestorJustificationRequired": false,
    "approvalMode": "NoApproval",
    "approvalStages": []
  }
}
```

## Step 3: Request access

In this step, the **Requestor1** user account requests access to the resources in the access package.

### Get access package assignment policies

Get the policy that is needed to request access to resources.

#### Request

```http
GET https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageAssignmentPolicies?$filter=(id eq '6c1f65ec-8c25-4a45-83c2-a1de2a6d0e9f')
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageAssignmentPolicies",
  "value": [
    {
      "id": "6c1f65ec-8c25-4a45-83c2-a1de2a6d0e9f",
      "accessPackageId": "cf54c6ca-d717-49bc-babe-d140d035dfdd",
      "displayName": "direct",
      "description": "direct assignments by administrator",
      "canExtend": false,
      "durationInDays": 30,
      "expirationDateTime": null,
      "createdBy": "admin@contoso.onmicrosoft.com",
      "createdDateTime": "2020-06-29T19:47:44.74Z",
      "modifiedBy": "admin@contoso.onmicrosoft.com",
      "modifiedDateTime": "2020-06-29T19:47:44.757Z",
      "accessReviewSettings": null,
      "requestorSettings": {
        "scopeType": "SpecificDirectorySubjects",
        "acceptRequests": true,
        "allowedRequestors": [
          {
            "@odata.type": "#microsoft.graph.singleUser",
            "isBackup": false,
            "id": "ce02eca8-752b-4ecf-ac29-aa9bccd87606",
            "description": "Requestor1"
          }
        ]
      },
      "requestApprovalSettings": {
        "isApprovalRequired": false,
        "isApprovalRequiredForExtension": false,
        "isRequestorJustificationRequired": false,
        "approvalMode": "NoApproval",
        "approvalStages": []
      }
    }
  ]
}
```

### Create an access package request

To request access to resources in the access package, you need to provide these values:
- **id** of the **Requestor1** user account that you created for the value of the **targetId** property
- **id** of the assignment policy for the value of the **assignmentPolicyId** property
- **id** of the access package for the value of **accessPackageId** property

In the response you can see the status of **Accepted** and a state of **Submitted**. Record the value of the **id** property that is returned to get the status of the request later.

#### Request

```http
POST https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageAssignmentRequests
Content-type: application/json

{
  "requestType": "AdminAdd",
  "accessPackageAssignment":{
     "targetId":"ce02eca8-752b-4ecf-ac29-aa9bccd87606",
     "assignmentPolicyId":"6c1f65ec-8c25-4a45-83c2-a1de2a6d0e9f",
     "accessPackageId":"cf54c6ca-d717-49bc-babe-d140d035dfdd"
  }
}
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageAssignmentRequests/$entity",
    "createdDateTime": null,
    "completedDate": null,
    "id": "a6bb6942-3ae1-4259-9908-0133aaee9377",
    "requestType": "AdminAdd",
    "requestState": "Submitted",
    "requestStatus": "Accepted",
    "isValidationOnly": false,
    "expirationDateTime": null,
    "justification": null
}
```

## Step 4: Validate that access has been assigned

In this step, you confirm that the **Requestor1** user account was assigned the access package and that they are now a member of the **Marketing resources** group.

### Get the status of the request

Use the value of the **id** property of the request to get the current status of it. In the response, you can see the status changed to **Fulfilled** and the state changed to **Delivered**.

#### Request

```http
GET https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageAssignmentRequests/a6bb6942-3ae1-4259-9908-0133aaee9377
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageAssignmentRequests/$entity",
  "createdDateTime": "2020-06-29T20:24:24.683Z",
  "completedDate": "2020-06-29T20:24:47.937Z",
  "id": "a6bb6942-3ae1-4259-9908-0133aaee9377",
  "requestType": "AdminAdd",
  "requestState": "Delivered",
  "requestStatus": "Fulfilled",
  "isValidationOnly": false,
  "expirationDateTime": null,
  "justification": null
}
```

### Get the members of the group

After the request has been granted, you can use the **id** that you recorded for the **Marketing resources** group to see that the **Requestor1** user account has been added to it.

#### Request

```http
GET https://graph.microsoft.com/beta/groups/a468eaea-ed6c-4290-98d2-a96bb1cb4209/members
```

#### Response:

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#directoryObjects",
  "value": [
    {
      "@odata.type": "#microsoft.graph.user",
      "id": "ce02eca8-752b-4ecf-ac29-aa9bccd87606",
      "deletedDateTime": null,
      "accountEnabled": true,
      "ageGroup": null,
      "businessPhones": [],
      "city": null,
      "createdDateTime": "2020-06-23T18:43:24Z",
      "creationType": null,
      "companyName": null,
      "consentProvidedForMinor": null,
      "country": null,
      "department": null,
      "displayName": "Requestor1",
      "employeeId": null,
      "faxNumber": null,
      "givenName": null,
      "imAddresses": [],
      "infoCatalogs": [],
      "isResourceAccount": null,
      "jobTitle": null,
      "legalAgeGroupClassification": null,
      "mail": null,
      "mailNickname": "Requestor1"
    }
  ]
}
```

### Get access package assignments

You can also use the **id** of the access package policy that you created to see that resources have been assigned to the **Requestor1** user account.

#### Request

```http
GET https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageAssignments?$filter=accessPackageAssignmentPolicy/Id eq '6c1f65ec-8c25-4a45-83c2-a1de2a6d0e9f'
```

#### Response

```http
{
  "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageAssignments",
  "value": [
    {
      "id": "66a38bed-733f-4127-aaeb-743c93cf4409",
      "catalogId": "ede67938-cda7-4127-a9ca-7c7bf86a19b7",
      "accessPackageId": "cf54c6ca-d717-49bc-babe-d140d035dfdd",
      "assignmentPolicyId": "6c1f65ec-8c25-4a45-83c2-a1de2a6d0e9f",
      "targetId": "2bc42425-6dc5-4f2a-9ebb-7a7464481eb0",
      "assignmentStatus": "Delivered",
      "assignmentState": "Delivered",
      "isExtended": false,
      "expiredDateTime": null
    }
  ]
}
```

## Step 5: Clean up resources

In this step, you remove the changes you made and delete the **Marketing Campaign** access package.

### Remove an access package assignment

You must remove any assignments to the access package before you can delete it. Use the **id** of the assignment request that you previously recorded to delete it.

#### Request

```http
POST https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageAssignmentRequests
Content-type: application/json

{
  "requestType": "AdminRemove",
  "accessPackageAssignment":{
     "id": "66a38bed-733f-4127-aaeb-743c93cf4409"
  }
}
```

#### Response

```http
{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#accessPackageAssignmentRequests/$entity",
    "createdDateTime": null,
    "completedDate": null,
    "id": "78eaee8c-e6cf-48c9-8f99-aae44c35e379",
    "requestType": "AdminRemove",
    "requestState": "Submitted",
    "requestStatus": "Accepted",
    "isValidationOnly": false,
    "expirationDateTime": null,
    "justification": null
}
```

### Delete the access package assignment policy

Use the **id** of the assignment policy that you previously recorded to delete it. Make sure all assignments are removed first.

#### Request

```http
DELETE https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackageAssignmentPolicies/6c1f65ec-8c25-4a45-83c2-a1de2a6d0e9f
```

#### Response

```http
No Content - 204 - 797ms
```

### Delete the access package

Use the **id** of the access package that you previously recorded to delete it.

#### Request

```http
DELETE https://graph.microsoft.com/beta/identityGovernance/entitlementManagement/accessPackages/cf54c6ca-d717-49bc-babe-d140d035dfdd
```

#### Response

```http
No Content - 204 - 594ms
```

### Delete the user accounts

Delete the **Requestor1** user account.

#### Request

```http
DELETE https://graph.microsoft.com/beta/users/ce02eca8-752b-4ecf-ac29-aa9bccd87606
```

#### Response

```http
No Content - 204 - 594ms
```

Delete the **Admin1** administrator account.

#### Request

```http
DELETE https://graph.microsoft.com/beta/users/792006a5-1d63-4d63-81c7-ec0808181486
```

#### Response

```http
No Content - 204 - 594ms
```

### Delete the group

Delete the **Marketing resources** group.

#### Request

```http
DELETE https://graph.microsoft.com/beta/groups/a468eaea-ed6c-4290-98d2-a96bb1cb4209
```

#### Response

```http
No Content - 204 - 594ms
```
