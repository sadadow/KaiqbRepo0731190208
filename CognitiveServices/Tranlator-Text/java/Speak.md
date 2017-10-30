## Get spoken text

The following code gets a stream of the source text being spoken in the given language, using the Speak method.

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
	static String path = "/V2/Http.svc/Speak";

	public static void get (URL url, String output_path) throws Exception {
		HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
		connection.setRequestMethod("GET");
		connection.setRequestProperty("Ocp-Apim-Subscription-Key", key);
		connection.setDoOutput(true);

		InputStream inputStream = connection.getInputStream();
		FileOutputStream outputStream = new FileOutputStream(output_path);

		int bytesRead = -1;
		byte[] buffer = new byte[1024];
		while ((bytesRead = inputStream.read(buffer)) != -1) {
			outputStream.write(buffer, 0, bytesRead);
		}

		outputStream.close();
		inputStream.close();

		return;
	}

	public static void Speak () throws Exception {
		String text = "Hello world";
		String language = "en-US";
		String output_path = "speak.wav";

		String url = host + path + "?text=" + URLEncoder.encode (text, "UTF-8") + "&language=" + language;
		URL url2 = new URL (url);

		get (url2, output_path);
    }

	public static void main(String[] args) {
		try {
			Speak ();
			System.out.println ("File downloaded.");
		}
		catch (Exception e) {
			System.out.println (e);
		}
	}
}
```

**Get spoken text response**

A successful response is returned as a .wav or .mp3 stream.
