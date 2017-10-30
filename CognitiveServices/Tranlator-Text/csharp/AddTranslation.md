## Add translation

The following code adds a translation to the translation memory, using the AddTranslation method. This is useful if you want to tailor the user's experience so they receive a certain translation for a given source text.

1. Create a new C# project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```csharp
using System;
using System.Net;
using System.Net.Http;

namespace TranslateTextQuickStart
{
    class Program
    {
        static string host = "https://api.microsofttranslator.com";
        static string path = "/V2/Http.svc/AddTranslation";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        async static void AddTranslation()
        {
            HttpClient client = new HttpClient();
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", key);

            string originalText = "Hi there";
            string translatedText = "Salut";
            string from = "en-US";
            string to = "fr-fr";
            string user = "JohnDoe";

            string uri = host + path +
                "?originalText=" + WebUtility.UrlEncode(originalText) +
                "&translatedText=" + WebUtility.UrlEncode(translatedText) +
                "&from=" + from +
                "&to=" + to +
                "&user=" + WebUtility.UrlEncode(user);

            HttpResponseMessage response = await client.GetAsync(uri);
            Console.WriteLine(response.ToString());
        }

        static void Main(string[] args)
        {
            AddTranslation();
            Console.ReadLine();
        }
    }
}
```

**Add translation response**

A successful response is simply returned as HTTP status code 200 (OK): 

```http
StatusCode: 200, ReasonPhrase: 'OK', Version: 1.1, Content: System.Net.Http.StreamContent, Headers:
{
  X-MS-Trans-Info: 1230.V2_Rest.AddTranslation.46F207D0
  Date: Fri, 27 Oct 2017 07:47:19 GMT
  Content-Length: 0
}
```
