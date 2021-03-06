---
title: User Group APIs
layout: default
nav_link: User Group APIs
nav_order: 460
nav_level: 3
lang: en
---
# <a name="userGroups" class="api-ref-title">User Group APIs</a>

**DEPRECATED:** These APIs have been deprecated. An exact date for removal will be confirmed before the end of 2017 but you should look to update your scripts as soon as possible.

```
POST /v2/usermanagement/{orgId}/user-groups
PUT /v2/usermanagement/{orgId}/user-groups/{groupId}
DELETE /v2/usermanagement/{orgId}/user-groups/{groupId}
```

<hr class="api-ref-rule">

You cannot create either user groups or product profiles through the API. You must create them in the [Admin Console](https://adminconsole.adobe.com/enterprise/). You can then use the User Management API to manage product access for users by adding and removing users to and from your existing user groups and product profiles.

You can use the a POST request to the [`action` resource](ActionsRef.md) for your organization to manage user group memberships, and to manage administrative rights in user groups. The _commands_ in the body of your POST request specify _action steps_ to take for a given _user_.

* [add](ActionsCmds.md#add) Add a user to a specified _usergroup_
* [remove](ActionsCmds.md#remove) Remove a user from a specified _usergroup_
* [addRoles](ActionsCmds.md#addRoles) Add the _admin_ role for a specified _usergroup_
* [removeRoles](ActionsCmds.md#removeRoles) Remove the _admin_ role for a specified _usergroup_ 


<hr class="api-ref-rule">
