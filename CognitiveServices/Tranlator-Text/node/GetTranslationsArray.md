## Get translations arrays

The following code gets arrays of translation candidates for multiple source texts, using the GetTranslationsArray method.

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
let path = '/V2/Http.svc/GetTranslationsArray';

let params = '';

let from = "en-us";
let to = "fr-fr";

let ns = "http://schemas.microsoft.com/2003/10/Serialization/Arrays";
let content =
	"<GetTranslationsArrayRequest>" +
	"  <AppId />" +
	"  <From>" + from + "</From>" +
	"  <Texts>" +
	"    <string xmlns=\"" + ns + "\">Hello</string>" +
	"    <string xmlns=\"" + ns + "\">Goodbye</string>" +
	"  </Texts>" +
	"  <To>" + to + "</To>" +
	"  <MaxTranslations>10</MaxTranslations>" +
	"</GetTranslationsArrayRequest>";

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

let GetTranslationsArray = function () {
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

GetTranslationsArray ();
```

**Get translations arrays response**

A successful response is returned in XML, as shown in the following example: 

```xml
<ArrayOfGetTranslationsResponse xmlns="http://schemas.datacontract.org/2004/07/Microsoft.MT.Web.Service.V2" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <GetTranslationsResponse>
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
        <Count>2</Count>
        <MatchDegree>100</MatchDegree>
        <MatchedOriginalText>Hello</MatchedOriginalText>
        <Rating>1</Rating>
        <TranslatedText>Bonjour,</TranslatedText>
      </TranslationMatch>
      <TranslationMatch>
        <Count>1</Count>
        <MatchDegree>100</MatchDegree>
        <MatchedOriginalText>Hello</MatchedOriginalText>
        <Rating>1</Rating>
        <TranslatedText>Bonjour</TranslatedText>
      </TranslationMatch>
      <TranslationMatch>
        <Count>1</Count>
        <MatchDegree>88</MatchDegree>
        <MatchedOriginalText>Hello?</MatchedOriginalText>
        <Rating>1</Rating>
        <TranslatedText>Tu es là ?</TranslatedText>
      </TranslationMatch>
      <TranslationMatch>
        <Count>1</Count>
        <MatchDegree>88</MatchDegree>
        <MatchedOriginalText>Hello?</MatchedOriginalText>
        <Rating>1</Rating>
        <TranslatedText>Vous êtes là ?</TranslatedText>
      </TranslationMatch>
      <TranslationMatch>
        <Count>1</Count>
        <MatchDegree>88</MatchDegree>
        <MatchedOriginalText>Hello,</MatchedOriginalText>
        <Rating>1</Rating>
        <TranslatedText>Salut</TranslatedText>
      </TranslationMatch>
      <TranslationMatch>
        <Count>1</Count>
        <MatchDegree>66</MatchDegree>
        <MatchedOriginalText>&lt;&lt;"Hello!</MatchedOriginalText>
        <Rating>1</Rating>
        <TranslatedText>&lt;&lt; "Bonjour !</TranslatedText>
      </TranslationMatch>
    </Translations>
  </GetTranslationsResponse>
  <GetTranslationsResponse>
    <From>en</From>
    <Translations>
      <TranslationMatch>
        <Count>0</Count>
        <MatchDegree>100</MatchDegree>
        <MatchedOriginalText />
        <Rating>5</Rating>
        <TranslatedText>Au revoir</TranslatedText>
      </TranslationMatch>
    </Translations>
  </GetTranslationsResponse>
</ArrayOfGetTranslationsResponse>
```

