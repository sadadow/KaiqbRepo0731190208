## Get spoken text

The following code gets a stream of the source text being spoken in the given language, using the Speak method.

1. Create a new Node.JS project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```nodejs
'use strict';

let fs = require ('fs');
let https = require ('https');

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'ENTER KEY HERE';

let host = 'api.microsofttranslator.com';
let path = '/V2/Http.svc/Speak';

let text = "Hello world";
let language = "en-US";

let params = "?text=" + encodeURI (text) + "&language=" + language;

let output_path = "speak.wav";

let response_handler = function (response) {
	let ws = fs.createWriteStream(output_path);
    response.on ('data', function (d) {
        ws.write (d);
    });
    response.on ('end', function () {
		ws.close ();
		console.log("File written.");
    });
    response.on ('error', function (e) {
        console.log ('Error: ' + e.message);
    });
};

let Speak = function () {
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

Speak ();
```

**Get spoken text response**

A successful response is returned as a .wav or .mp3 stream.

