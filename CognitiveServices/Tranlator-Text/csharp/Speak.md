## Get spoken text

The following code gets a stream of the source text being spoken in the given language, using the [Speak](http://docs.microsofttranslator.com/text-translate.html#!/default/get_Speak) method.

1. Create a new C# project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```csharp
using System;
using System.IO;
using System.Net;

namespace TranslateTextQuickStart
{
    class Program
    {
        static string host = "https://api.microsofttranslator.com";
        static string path = "/V2/Http.svc/Speak";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static void Speak()
        {
            string text = "Hello world";
            string language = "en-US";
            string output_path = "speak.wav";

            string uri = host + path + "?text=" + System.Net.WebUtility.UrlEncode(text) + "&language=" + language;

            WebRequest webRequest = WebRequest.Create(uri);
            webRequest.Headers.Add("Ocp-Apim-Subscription-Key", key);

            using (WebResponse response = webRequest.GetResponse())
            using (Stream stream = response.GetResponseStream())
            using (var fileStream = File.Create(output_path))
            {
                stream.CopyTo(fileStream);
                Console.WriteLine("File written.");
            }
        }

        static void Main(string[] args)
        {
            Speak();
            Console.ReadLine();
        }
    }
}
```

**Get spoken text response**

A successful response is returned as a .wav or .mp3 stream.
