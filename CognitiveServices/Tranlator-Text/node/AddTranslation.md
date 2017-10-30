## Add translation

The following code adds a translation to the translation memory, using the AddTranslation method. This is useful if you want to tailor the user's experience so they receive a certain translation for a given source text.

1. Create a new Node.JS project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```nodejs
'use strict';

let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'api.microsofttranslator.com';
let path = '/V2/Http.svc/AddTranslation';

let originalText = "Hi there";
let translatedText = "Salut";
let from = "en-US";
let to = "fr-fr";
let user = "JohnDoe";

let params =
	"?originalText=" + encodeURI (originalText) +
	"&translatedText=" + encodeURI (translatedText) +
	"&from=" + from +
	"&to=" + to +
	"&user=" + encodeURI (user);

let response_handler = function (response) {
    let body = '';
    response.on ('data', function (d) {
        body += d;
    });
    response.on ('end', function () {
		console.log (body);
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

let AddTranslation = function () {
	let request_params = {
		method : 'GET',
		hostname : host,
		path : path + params,
		headers : {
			'Ocp-Apim-Subscription-Key' : subscriptionKey,
		}
	};

	let req = https.request (request_params, response_handler);
	req.end ();
}

AddTranslation ();
```

**Add translation response**

A successful response is simply returned as HTTP status code 200 (OK).

