## Add translation array

The following code adds an array of translations to the translation memory, using the [AddTranslationArray](http://docs.microsofttranslator.com/text-translate.html#!/default/post_AddTranslationArray) method. This is useful if you want to tailor the user's experience so they receive certain translations for given source texts.

1. Create a new C# project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```csharp
using System;
using System.Net.Http;
using System.Text;
using System.Xml.Linq;

namespace TranslateTextQuickStart
{
    class Program
    {
        static string host = "https://api.microsofttranslator.com";
        static string path = "/V2/Http.svc/AddTranslationArray";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        async static void AddTranslationArray()
        {
            string uri = host + path;

            XNamespace ns = @"http://schemas.datacontract.org/2004/07/Microsoft.MT.Web.Service.V2";
            XDocument doc = new XDocument(
                new XElement("AddtranslationsRequest",
                    // NOTE: AppId is required, but it can be empty because we are sending the Ocp-Apim-Subscription-Key header.
                    new XElement("AppId"),
                    new XElement("From", "en-US"),
                    new XElement("Options",
                        new XElement(ns + "User", "JohnDoe")
                    ),
                    new XElement("To", "fr-fr"),
                    new XElement("Translations",
                        new XElement(ns + "Translation",
                            new XElement(ns + "OriginalText", "Hi there"),
                            new XElement(ns + "Rating", 1),
                            new XElement(ns + "TranslatedText", "Salut")
                        )
                    )
                )
            );
            var requestBody = doc.ToString();

            using (var client = new HttpClient())
            using (var request = new HttpRequestMessage())
            {
                request.Method = HttpMethod.Post;
                request.RequestUri = new Uri(uri);
                request.Content = new StringContent(requestBody, Encoding.UTF8, "text/xml");
                request.Headers.Add("Ocp-Apim-Subscription-Key", key);
                var response = await client.SendAsync(request);
                Console.WriteLine(response.ToString());
            }
        }

        static void Main(string[] args)
        {
            AddTranslationArray();
            Console.ReadLine();
        }
    }
}
```

**Add translation array response**

A successful response is simply returned as HTTP status code 200 (OK): 

```http
StatusCode: 200, ReasonPhrase: 'OK', Version: 1.1, Content: System.Net.Http.StreamContent, Headers:
{
  X-MS-Trans-Info: 0639.V2_Rest.AddTranslationArray.467960AD
  Date: Fri, 27 Oct 2017 02:00:46 GMT
  Content-Length: 0
}
```
