## Get translations

The following code gets an array of translation candidates for the source text, using the GetTranslations method.

1. Create a new Java project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```java
import java.io.*;
import java.net.*;
import java.util.*;
import javax.net.ssl.HttpsURLConnection;

public class TranslateTextQuickStart {

// **********************************************
// *** Update or verify the following values. ***
// **********************************************

// Replace the key string value with your valid subscription key.
	static String key = "ENTER KEY HERE";

	static String host = "https://api.microsofttranslator.com";
	static String path = "/V2/Http.svc/GetTranslations";

	public static String post (URL url, String content) throws Exception {
		HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
		connection.setRequestMethod("POST");
		connection.setRequestProperty("Content-Type", "text/xml");
		connection.setRequestProperty("Ocp-Apim-Subscription-Key", key);
		connection.setDoOutput(true);

        DataOutputStream wr = new DataOutputStream(connection.getOutputStream());
		byte[] encoded_content = content.getBytes("UTF-8");
		wr.write(encoded_content, 0, encoded_content.length);
		wr.flush();
		wr.close();

		StringBuilder response = new StringBuilder ();
		BufferedReader in = new BufferedReader(
		new InputStreamReader(connection.getInputStream()));
		String line;
		while ((line = in.readLine()) != null) {
			response.append(line);
		}
		in.close();

		return response.toString();
	}

	public static String GetTranslations () throws Exception {

		String from = "en-us";
		String to = "fr-fr";
		String text = "Hi there";
		String maxTranslations = "10";
		String url = host + path + "?from=" + from + "&to=" + to + "&maxTranslations=" + maxTranslations + "&text=" + URLEncoder.encode (text, "UTF-8");
		URL url2 = new URL (url);

		return post (url2, "");
    }

	public static void main(String[] args) {
		try {
			String response = GetTranslations ();
			System.out.println (response);
		}
		catch (Exception e) {
			System.out.println (e);
		}
	}
}
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
