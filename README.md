# OpenMinds JavaScript Library

This library allows web apps to authenticate users through the OpenMinds oAuth flow. You need to download the .js and .html files and make them accessible through your web server. No further server configuration is needed to use the library.

## Setup
- Download `openminds_connect.min.js` and `oauth_redirect.html` and add them to your web app.
- Include `openminds_connect.min.js` with a script tag in your web app:
test:
    <script src="openminds_connect.js" type="text/javascript"></script>
- Make `oauth_redirect.html` accessible through your web app with a URL path.
- Register your app with OpenMinds at [http://openminds.io/developers/apps](http://openminds.io/developers/apps) by clicking "Create New App". Give your app a name & description, and fill in the URL to `oauth_redirect.html` in the "oAuth Callback URL" field.
- Note the ID listed in the "App ID" field.

## Usage
- The library exposes two methods: `om.logIn` and `om.logOut`.


See [http://github.com/Root-1/flashcards/](http://github.com/Root-1/flashcards/) for an app that uses the library to authenticate users and pull lists using the OpenMinds API.
