## Get translations

The following code gets an array of translation candidates for the source text, using the GetTranslations method.

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
let path = '/V2/Http.svc/GetTranslations';

let from = "en-us";
let to = "fr-fr";
let text = "Hi there";
let maxTranslations = "10";
let params = "?from=" + from + "&to=" + to + "&maxTranslations=" + maxTranslations + "&text=" + encodeURI (text);

let content = '';

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

let GetTranslations = function () {
	let request_params = {
		method : 'POST',
		hostname : host,
		path : path + params,
		headers : {
			'Content-Type' : 'text/xml',
			'Ocp-Apim-Subscription-Key' : subscriptionKey,
		}
	};

	let req = https.request (request_params, response_handler);
	req.write (content);
	req.end ();
}

GetTranslations ();
```

**Get translations response**

A successful response is returned in XML, as shown in the following example: 

```xml
<GetTranslationsResponse xmlns="http://schemas.datacontract.org/2004/07/Microsoft.MT.Web.Service.V2" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <From>en</From>
  <Translations>
    <TranslationMatch>
      <Count>0</Count>
      <MatchDegree>100</MatchDegree>
      <MatchedOriginalText />
      <Rating>5</Rating>
      <TranslatedText>Salut</TranslatedText>
    </TranslationMatch>
    <TranslationMatch>
      <Count>1</Count>
      <MatchDegree>100</MatchDegree>
      <MatchedOriginalText>Hi there</MatchedOriginalText>
      <Rating>1</Rating>
      <TranslatedText>Salut</TranslatedText>
    </TranslationMatch>
  </Translations>
</GetTranslationsResponse>
```
