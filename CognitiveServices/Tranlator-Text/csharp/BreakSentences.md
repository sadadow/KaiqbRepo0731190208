## Break sentences

The following code breaks the source text into sentences, using the BreakSentences method.

1. Create a new C# project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```csharp
using System;
using System.IO;
using System.Net;
using System.Net.Http;
using System.Runtime.Serialization;
using System.Text;

namespace TranslateTextQuickStart
{
    class Program
    {
        static string host = "https://api.microsofttranslator.com";
        static string path = "/V2/Http.svc/BreakSentences";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        async static void BreakSentences()
        {
            HttpClient client = new HttpClient();
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", key);

            string text = "Here is a sentence. Here is another sentence. Here is a third sentence.";
            string language = "en-US";

            string uri = host + path +
                "?text=" + WebUtility.UrlEncode(text) +
                "&language=" + language;

            HttpResponseMessage response = await client.GetAsync(uri);
            string result = await response.Content.ReadAsStringAsync();
            Console.WriteLine(result);

            // NOTE: Use the following code to deserialize the stream contents.
            /*
            DataContractSerializer dcs = new DataContractSerializer(Type.GetType("System.Int32[]"));
            MemoryStream memoryStream = new MemoryStream(Encoding.UTF8.GetBytes(result));
            int[] languageNames = (int[])dcs.ReadObject(memoryStream);
            foreach (var i in languageNames)
            {
                Console.WriteLine(i);
            }
            */
        }

        static void Main(string[] args)
        {
            BreakSentences();
            Console.ReadLine();
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
