## Break sentences

The following code breaks the source text into sentences, using the BreakSentences method.

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
	static String path = "/V2/Http.svc/BreakSentences";

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

	public static String BreakSentences () throws Exception {
		String text = "Here is a sentence. Here is another sentence. Here is a third sentence.";
        String language = "en-US";

		String url = host + path +
			"?text=" + URLEncoder.encode (text, "UTF-8") +
			"&language=" + language;

		URL url2 = new URL (url);
		return get (url2);
    }

	public static void main(String[] args) {
		try {
			String response = BreakSentences ();
			System.out.println (response);
		}
		catch (Exception e) {
			System.out.println (e);
		}
	}
}
```

**Break sentences response**

A successful response is returned in XML, as shown in the following example: 

```xml
<ArrayOfint xmlns="http://schemas.microsoft.com/2003/10/Serialization/Arrays" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <int>20</int>
  <int>26</int>
  <int>25</int>
</ArrayOfint>
```

