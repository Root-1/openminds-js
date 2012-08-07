# OpenMinds JavaScript Library

This library allows web apps to authenticate users through the OpenMinds oAuth flow.
It will open a popup window and ask the user to sign in to OpenMinds (if they are not already).
If this is the first time the user is launching your app, they will need to allow access to the app.
If access is granted, the web app will receive an OpenMinds access token that can be used to make API calls on behalf of the authenticated user.
You need to download the .js and .html files and make them accessible through your web server. No further server configuration is needed to use the library.

## Setup
- Download `openminds_connect.min.js` and `oauth_redirect.html` and add them to your web app.
- Include `openminds_connect.min.js` with a script tag in your web app:
    ```<script src="openminds_connect.min.js" type="text/javascript"></script>```
- Make `oauth_redirect.html` accessible through your web app with a URL path.
- Register your app with OpenMinds at [http://openminds.io/developers/apps](http://openminds.io/developers/apps) by clicking "Create New App". Give your app a name & description, and fill in the URL to `oauth_redirect.html` in the "oAuth Callback URL" field.
- Note the ID listed in the "App ID" field.

## Usage
The library exposes two methods: `om.logIn` and `om.logOut`.

### om.logIn
`om.logIn` takes an `options` object with the following required properties:
- `appId`: the ID of the app registered with OpenMinds.
- `redirectUri`: the URL of the `oauth_redirect.html` file served from the same domain as the web app. This must match the `oAuth Callback URL` for the app registered in OpenMinds.
- `callback`: the function that gets called after successful authentication and app authorization. If the user authorizes the app, an access token will be passed to the callback function.

```
    om.logIn({
      // Use your App ID here
      appId: '4fe3add7b767722981000016',
      // Must match the oAuth redirect URI specified for your app
      redirectUri: 'http://myapp.com/oauth_callback',
      // accessToken is null if user does not authorize the app
      // or closes the popup window.
      callback: function(accessToken) {
        if (accessToken) {
          // We have the access token and can make API calls.
          loadApp(accessToken);
        }
      }
    });
```

Once you have an OpenMinds Access Token in the callback, you can start making API calls. (The API supports cross-origin requests from browsers).

### om.logOut
A call to `om.logOut` will clear out the access token from the browser and log the user out of OpenMinds.
```
om.logOut(function() {
  exitApp();
});
```

## Example
See [http://github.com/Root-1/flashcards](http://github.com/Root-1/flashcards) for an app that uses the library to authenticate users and pull lists using the OpenMinds API.
