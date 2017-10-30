## Add translation

The following code adds a translation to the translation memory, using the AddTranslation method. This is useful if you want to tailor the user's experience so they receive a certain translation for a given source text.

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
	static String path = "/V2/Http.svc/AddTranslation";

	public static String get (URL url) throws Exception {
		HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
		connection.setRequestMethod("GET");
		connection.setRequestProperty("Ocp-Apim-Subscription-Key", key);
		connection.setDoOutput(true);

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

	public static String AddTranslation () throws Exception {
		String originalText = "Hi there";
		String translatedText = "Salut";
		String from = "en-US";
		String to = "fr-fr";
		String user = "JohnDoe";

		String url = host + path +
			"?originalText=" + URLEncoder.encode (originalText, "UTF-8") +
			"&translatedText=" + URLEncoder.encode (translatedText, "UTF-8") +
			"&from=" + from +
			"&to=" + to +
			"&user=" + URLEncoder.encode (user, "UTF-8");

		URL url2 = new URL (url);
		return get (url2);
    }

	public static void main(String[] args) {
		try {
			String response = AddTranslation ();
			System.out.println (response);
		}
		catch (Exception e) {
			System.out.println (e);
		}
	}
}
```

**Add translation response**

A successful response is simply returned as HTTP status code 200 (OK).
