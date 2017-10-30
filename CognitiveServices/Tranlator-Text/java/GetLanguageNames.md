## Get language names

The following code gets friendly names for multiple languages, using the GetLanguageNames method.

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

    static String locale = "en";
	static String host = "https://api.microsofttranslator.com";
	static String path = "/V2/Http.svc/GetLanguageNames?locale=" + locale;

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

	public static String GetLanguageNames () throws Exception {
		URL url = new URL (host + path);
		String ns = "http://schemas.microsoft.com/2003/10/Serialization/Arrays";
		String xml =
			"<ArrayOfstring xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/2003/10/Serialization/Arrays\">" +
            "    <string>en</string>" +
            "    <string>fr</string>" +
            "    <string>uk</string>" +
            "</ArrayOfstring>";

		return post (url, xml);
    }

	public static void main(String[] args) {
		try {
			String response = GetLanguageNames ();
			System.out.println (response);
		}
		catch (Exception e) {
			System.out.println (e);
		}
	}
}
```

**Get language names response**

A successful response is returned in XML, as shown in the following example: 

```xml
<ArrayOfstring xmlns="http://schemas.microsoft.com/2003/10/Serialization/Arrays" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <string>English</string>
  <string>French</string>
  <string>Ukrainian</string>
</ArrayOfstring>
```

