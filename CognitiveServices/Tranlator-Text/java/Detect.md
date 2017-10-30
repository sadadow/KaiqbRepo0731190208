## Detect language

The following code identifies the language of the source text, using the Detect method.

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
	static String path = "/V2/Http.svc/Detect";

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

	public static String Detect () throws Exception {
		String text = "Hello world";
		String url = host + path + "?text=" + URLEncoder.encode (text, "UTF-8");
		URL url2 = new URL (url);
		return get (url2);
    }

	public static void main(String[] args) {
		try {
			String response = Detect ();
			System.out.println (response);
		}
		catch (Exception e) {
			System.out.println (e);
		}
	}
}
```

**Detect language response**

A successful response is returned in XML, as shown in the following example: 

```xml
<string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">en</string>
```
