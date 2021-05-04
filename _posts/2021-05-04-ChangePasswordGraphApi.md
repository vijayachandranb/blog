---
layout: post
title: Change password with MS Graph Api
---

## Change user password in Azure AD B2C with MS Graph Api
You can reset a user's password in Azure AD B2C without user interaction by using Microsoft's graph api. Azure AD B2C comes with user flows to reset a user's password out of the box. But there can be a scenario where we need to provide a password change option from within our app for the users without redirecting them to B2C pages. This is the case where Microsoft's graph api comes handy. Here's how it's done.

### Register an app in Azure AD B2C

Register a new application from **App Registrations** by giving a name and selecting single tenant as in the below image

<img src="{{ site.baseurl }}/images/GraphApiReg.PNG"/>

Please make sure to select the checkbox which says **Grant admin consent to openid and offline_access permissions** and click "Register" to create your app. Now got to regsitered app and create a secret key from "Certificates and secrets" from the menu. Please make sure to note the secret key since you won't be able to see it again if you navigate to another route. You can also get the "Application (client) ID" from the Overview menu. You will be needing this Client ID and Secret key for api calls.

### Give User Administration role

This is an important step inorder for the app to do AD user manipulations. Go to "Roles and administrators" section from the left menu in Azure AD B2C and search for user administration. It will display the role below. Select the role and click "Add assignments". It will open a pop up. Search the app name you just created, select it and click Add.
You have now given "User Administration" role to the app you have just created. The app is good to go now.

### Use postman or fiddler to test

**1. Acquire Token**  
Use the below post request to acquire token
`https://login.microsoftonline.com/<your_tenant>/oauth2/v2.0/token`

Replace "<your_tenant>" with your tenant name
Use your app's client id, client secret to do a post request as shown in the image below

<img src="{{ site.baseurl }}/images/PostmanGraphApiToken.PNG"/>

grant_type should be "client_credentials" and scope should be "https://graph.microsoft.com/.default". You will get an access token for a successful post request.

**2. Change password**  
You can now do a patch request to `https://graph.microsoft.com/v1.0/users/<UserObjectId>` with the following request body along with the access token acquired from the previous request to change the user's password.
 Please make sure you replace <UserObjectId> with a valid guid of the user which is the unique identifier of the user in an azure ad.

 <img src="{{ site.baseurl }}/images/PostmanGraaphApiPasswordReset.PNG"/>

 The token acquired from previous request should be appended as an authorization bearer token request header.

 A successful password reset returns a 204 No content Http status.

 Hope this helps. Please visit my [blog](https://vijayachandranb.github.io/blog) for more tech posts.
