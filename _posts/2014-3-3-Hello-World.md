---
layout: post
title: Change password with MS Graph Api
---

## Change user password in Azure AD B2C with MS Graph Api
You can reset a user's password in Azure AD B2C without user interaction by using Microsoft's graph api. Azure AD B2C comes with user flows to reset a user's password out of the box. But there can be a scenario where we need to provide a password change option from within our app for the users without redirecting them to B2C pages. This is the case where Microsoft's graph api comes handy. Here's how it's done.

### Register an app in Azure AD B2C

Register a new application from **App Registrations** by giving a name and selecting single tenant as in the below image

<img src="{{ site.baseurl }}/images/GraphApiReg.PNG"/>

