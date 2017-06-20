# App ID Profiles Introduciton

## Introduction
You can use App ID to store your app user’s preferences. The App ID sample demonstrates how a fictional amusement park, Bluemix Land, can use App ID to help their users find restaurants in the park based on their food preferences.

When you run the sample, you will see how the App ID profiles feature stores the food preferences of the Bluemix Land app users. We will also explain how the profiles feature works.

## Running the app on Bluemix


In the following section we will walk you through how to set up your sample application and explain some behind the scenes code. You can download the sample app and try using it as an anonymous user, or login with an identity provider to learn about the different state that App ID can support.




## Initializing the App ID SDK

In order to use the service, you must initialize the SDK. 

1.	Set your Bluemix region to match the region in which your service instance was created.
2.	Be sure the tenant ID in your app is equal to the tenant ID found in your service credentials. 

## Anonymous login

If a user were to download the Bluemix Land app and start using it without logging in, you can still store information about them. The anonymous login API can be used to create an anonymous profile for the user.

1.	An anonymous login creates a new user profile in App ID.
2.	App ID generates an identity token and an access token.
a.	The access token is valid for a 30 day period.
b.	Logging in anonymously from the same device, with the same access token, extends its expiry by 30 days.
3.	Profile attributes can be accessed by using the access token. Tokens are held in appIDAuthorizationManager.


## The login widget

You can customize your application by using the login widget. The widget displays a list of supported identity providers – Facebook and Google.


1.	Configure your identity providers in the login widget tab of your service dashboard. 
2.	At the first login, a new profile is created and assigned an identity token. If the Identity already exists, the tokens of the existing profile are used.


## Getting Identity provider data

A user can give your app access to information, such as their name and profile picture, when they login through a third-party identity provider.


1.	The identity token contains the information received from the external identity provider.
2.	The token is stored as IdentityToken in appIDAuthorizationManager.

## Accessing attributes

In the sample, we asked users to tell us what kind of food they liked to eat – burgers, sandwiches, or pizza. Based on their answer, we can recommend restaurants they may enjoy during their time at Bluemix Land. Whether they are using the app anonymously or they have logged in, their selections are saved in their user profile. If they update their preferences, their new selections are saved.

## Progressive authentication

Progressive authentication occurs when a user begins as an anonymous user and then logs in for the first time by using an identity provider.

1.	The App Id SDK sends a request to login with an anonymous access token.
2.	The service attempts to find a profile for an identity received from an identity provider.
a.	If a profile exists, the service returns an access token for the identified profile.
b.	If no profile is found, the anonymous profile is assigned the anonymous access token.




## Storing tokens

You may want to store an anonymous users access token so that their selections are saved for their next visit to Bluemix land. By default, an anonymous token lives for 30 days. It’s expiration is only extended if the user access the app again with the 30 day period.

### For Android:

The token is stored in the shared preferences using “private” mode. This does not protect it from being read on a rooted device. Since identity tokens contain private information, we store only the access token, which has a short expiry time.

### For iOS:

A keychain is used to store the access token. The keychain offers develops extra security features, such as forcing the user to supply a fingerprint to retrieve data.


## Associating external information with a user

You can associate information not managed or stored in App ID with a user profile.

1.	Store the link to a remote file as an attribute.
2.	Store the ID of an entry in a remote database as an attribute.
