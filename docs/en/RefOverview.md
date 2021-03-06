---
title: API Reference
layout: page
nav_link: API Reference
nav_order: 300
nav_level: 1
lang: en
---

{% include_relative partials/umIntro.md %}

* [Connecting to the User Management API](#connect)
* [User Management Calls](#user-management-calls)

## <a name="connect" class="api-ref-subtitle">Connecting to the User Management API</a>

To establish a secure user-management session, you create a JSON Web Token (JWT) that encapsulates your identity information and exchange it for an IMS access token. Please see the [Prerequisites](getstarted.md#prereq) section of the [Getting Started Guide](getstarted.md) for detailed information about obtaining an access token.

* A typical access token is valid for 24 hours after it is issued.
* You can request multiple access tokens. Previous tokens are not invalidated when a new one is issued. You can authorize requests with any valid access token. This allows you to overlap access tokens to ensure your integration is always able to connect to Adobe.

Every call to the User Management API endpoints must be authorized with this access token in the `Authorization` header, along with the _API key_ for your client, which you received when you created the integration in the [Adobe I/O Console](https://console.adobe.io/).

For an example of a Python script that creates a JWT and exchanges it for an _access token_, see the [User Management Walkthrough](samples/index.md).

***********

## <a name="user-management-calls" class="api-ref-subtitle">User Management API Calls</a>

An application can use the User Management API to access Adobe users and manage their identities. You can create and remove user accounts for your organization, modify a user's personal information (depending on the account type), and modify users' access rights to Adobe applications within your organization.

Address all user-management requests to the UM API server:

```
https://usermanagement.adobe.io/v2/usermanagement/...
```

************

### Summary of Actions on Users

| Task | Operation | Endpoint | Description |
| :--- | :--- | :---| :---------- |
| [Create and Add Users](#add) | POST | `action/{orgId}`  | Create or add users to an organization by specifying a _command_ in the request body.  |
| [Update User Records](#update) | POST | `action/{orgId}`  | Update existing user records  |
| [Remove Users](#remove) |  DELETE | `action/{orgId}`  | Remove users from your organization |
| [Access Users](#users) | GET | various endpoints | List users in organization or in group, get individual user records  |
{:.bordertablestyle}

#### <a name="add" class="api-ref-subtitle">Create and Add Users</a>

{% include_relative partials/manageUsers.md %}

The POST [action](api/ActionsRef.md) API allows an Organization to create or add users to an organization by specifying a _command_ in the request body.

* For syntax details of the POST request and response, see [User Management Action Requests](api/ActionsRef.md).
* For details of the JSON command structure and defined actions, see [User Management Action Commands](api/ActionsCmds.md).
  + [Add an Adobe ID to your organization](api/ActionsCmds.md#addAdobeID)
  + [Create an Adobe-hosted Enterprise ID for your organization](api/ActionsCmds.md#createEnterpriseID)
  + [Create a Federated ID in a domain owned by your organization.](api/ActionsCmds.md#createFederatedID)

#### <a name="update" class="api-ref-subtitle">Update Users</a>

You can update personal information for a user who has an Enterprise or Federated ID that is managed by your organization through the POST [action](api/ActionsRef.md) API using the _update command_ in the request body. The following link details the command but it is recommended to read the full [API Actions Reference](api/ActionsRef.md) first.

* [Update an Enterprise or Federated user](api/ActionsCmds.md#update)

#### <a name="remove" class="api-ref-subtitle">Remove Users</a>

UM API allows an organization to remove a user from an organization, or from a Trusted Domain through the POST [action](api/ActionsRef.md) API. The _removeFromOrg command_ removes the user from the organization and from any product profiles and user-groups in the organization. An organization can also delete user accounts of type Enterprise and Federated ID, if the caller is from the owning organization and has delete access. This will also remove them from all product profiles and user-groups in a given domain.

* [Remove a user from the organization](api/ActionsCmds.md#removeFromOrg)

#### <a name="users" class="api-ref-subtitle">Access Users</a>

Retrieve user information for an organization or for members of user-groups and product profiles through the following GET APIs:

* [Get all users in an organization](api/getUsersWithPage.md)
* [Get a user](api/getUser.md)
* [Get users in a group or profile](api/getUsersByGroup.md)

## Summary of Actions on Groups

| Task | Operation | Endpoint | Description |
| :--- | :--- | :---| :---------- |
| [Access User Groups](#usergroups_access)| GET | `users/{orgId}/usergroups` | Get information about user groups |
| [Manage User Groups](#usergroups) | POST | `action/{orgId}`  | Manage group membership by performing actions on a _usergroup_ in the _commands_ structure.  |
{:.bordertablestyle}

### <a name="usergroups_access" class="api-ref-subtitle"> Access User Groups

Use a GET request to `users/{orgId}/{page}/{groupName}`

* [Get all user groups in an Organization](api/QueryUserGroups.md)  
* [Get details of a particular user group](api/group.md)
* [Get a list of users in a user group](api/getUsersByGroup.md)

### <a name="usergroups" class="api-ref-subtitle">Manage User-Groups</a>

Use the POST [action](api/ActionsRef.md) to manage user group membership and administrative rights.  

* [Add a user to a user group](api/ActionsCmds.md#add) in the _users_ field of the _add_ action for a _usergroup_
* [Remove a user from a user group](api/ActionsCmds.md#remove) with the _remove_ action for a _user_, in the _users_ field of a _remove_ action for a _usergroup_
* [Add User-group Administrator permissions for a user](api/ActionsCmds.md#addRoles) with the _addRoles_ action for a _user_
* [Remove User-group Administrator permissions for a user](api/ActionsCmds.md#removeRoles) with the _removeRoles_ action for a _user_

## Summary of Provisioning Actions

| Task | Operation | Endpoint | Description |
| :--- | :--- | :---| :---------- |
| [Provision Users](#provision) | POST | `action/{orgId}`  | Manage group memberships to control user access to products |
| [Access Products and Product Profiles](api/product.md) | GET | `{orgId}/products`  | List products  |
| [Manage Product Admin Rights](#admin) | POST | `action/{orgId}`  | Manage permissions by setting user roles  |
{:.bordertablestyle}

### <a name="provision" class="api-ref-subtitle">Provision Users</a>

{% include_relative partials/manageProductAccess.md %}

Use the POST [action](api/ActionsRef.md) API to manage provisioning by adding and removing users to and from User Groups and Product Profiles.

* [Provision a user to a product profile](api/ActionsCmds.md#add)
* [Remove provisioning of a user from a product profile](api/ActionsCmds.md#remove)
* [Add a user-group to a product profile](api/ActionsCmds.md#add)
* [Remove a user-group from a product profile](api/ActionsCmds.md#remove)
* [Add a user to a user-group](api/ActionsCmds.md#add)
* [Remove a user from a user-group](api/ActionsCmds.md#remove)

### <a name="admin" class="api-ref-subtitle">Manage Administrative Rights for Products</a>

Use the POST [action](api/ActionsRef.md) API to manage administrative rights for Adobe users in your organization. Possible roles include:
  * "org": The user is a [System Administrator](api/glossary.md#orgAdmin).
  * "deployment": The user is a [Deployment Administrator](api/glossary.md#deployment).
  * "{product-profile-name}": The user is a [Product Profile Administrator](api/glossary.md#productProfileAdmin).
  * "{user-group-name}": The user is a [UserGroup Administrator](api/glossary.md#usergroupAdmin).
  * "support": The user is a [Support Administator](api/glossary.md#supportAdmin). 

Use the _addRoles_ and _removeRoles_ actions in a _user_ command to manage administrator rights:

* [Add System Administrator permissions to a user](api/ActionsCmds.md#addRoles)
* [Remove System Administrator permissions to a user](api/ActionsCmds.md#removeRoles)
* [Add Deployment Administrator permissions to a user](api/ActionsCmds.md#addRoles)
* [Remove Deployment Administrator permissions to a user](api/ActionsCmds.md#removeRoles)
* [Add Support Administrator permissions to a user](api/ActionsCmds.md#addRoles)
* [Remove Support Administrator permissions to a user](api/ActionsCmds.md#removeRoles)
* [Add Product Administrator permissions to a user](api/ActionsCmds.md#addRoles)
* [Remove Product Administrator permissions to a user](api/ActionsCmds.md#removeRoles)
* [Add Product Profile Administrator permissions to a user](api/ActionsCmds.md#addRoles)
* [Remove Product Profile Administrator permissions to a user](api/ActionsCmds.md#removeRoles)
