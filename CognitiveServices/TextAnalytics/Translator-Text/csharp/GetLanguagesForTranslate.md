## Get supported languages for translation

The following code gets a list of language codes representing languages supported for translation, using the GetLanguagesForTranslate method.

1. Create a new C# project in your favorite IDE.
2. Add the code provided below.
3. Replace the `key` value with an access key valid for your subscription.
4. Run the program.

```csharp
using System;
using System.IO;
using System.Net.Http;
using System.Runtime.Serialization;
using System.Text;

namespace TranslateTextQuickStart
{
    class Program
    {
        static string host = "https://api.microsofttranslator.com";
        static string path = "/V2/Http.svc/GetLanguagesForTranslate";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        async static void GetLanguagesForTranslate()
        {
            HttpClient client = new HttpClient();
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", key);

            string uri = host + path;

            HttpResponseMessage response = await client.GetAsync(uri);

            string result = await response.Content.ReadAsStringAsync();
            Console.WriteLine(result);

            // NOTE: Use the following code to deserialize the stream contents.
            /*
            DataContractSerializer dcs = new DataContractSerializer(Type.GetType("System.String[]"));
            MemoryStream memoryStream = new MemoryStream(Encoding.UTF8.GetBytes(result));
            string[] languageNames = (string[])dcs.ReadObject(memoryStream);
            foreach (var i in languageNames)
            {
                Console.WriteLine(i);
            }
            */
        }

        static void Main(string[] args)
        {
            GetLanguagesForTranslate();
            Console.ReadLine();
        }
    }
}
```

**Get supported languages for translation response**

A successful response is returned in XML, as shown in the following example: 

```xml
<ArrayOfstring xmlns="http://schemas.microsoft.com/2003/10/Serialization/Arrays" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <string>af</string>
  <string>ar</string>
  <string>bn</string>
  <string>bs-Latn</string>
  <string>bg</string>
  <string>ca</string>
  <string>zh-CHS</string>
  <string>zh-CHT</string>
  <string>yue</string>
  <string>hr</string>
  <string>cs</string>
  <string>da</string>
  <string>nl</string>
  <string>en</string>
  <string>et</string>
  <string>fj</string>
  <string>fil</string>
  <string>fi</string>
  <string>fr</string>
  <string>de</string>
  <string>el</string>
  <string>ht</string>
  <string>he</string>
  <string>hi</string>
  <string>mww</string>
  <string>hu</string>
  <string>id</string>
  <string>it</string>
  <string>ja</string>
  <string>sw</string>
  <string>tlh</string>
  <string>tlh-Qaak</string>
  <string>ko</string>
  <string>lv</string>
  <string>lt</string>
  <string>mg</string>
  <string>ms</string>
  <string>mt</string>
  <string>yua</string>
  <string>no</string>
  <string>otq</string>
  <string>fa</string>
  <string>pl</string>
  <string>pt</string>
  <string>ro</string>
  <string>ru</string>
  <string>sm</string>
  <string>sr-Cyrl</string>
  <string>sr-Latn</string>
  <string>sk</string>
  <string>sl</string>
  <string>es</string>
  <string>sv</string>
  <string>ty</string>
  <string>ta</string>
  <string>th</string>
  <string>to</string>
  <string>tr</string>
  <string>uk</string>
  <string>ur</string>
  <string>vi</string>
  <string>cy</string>
</ArrayOfstring>
```
  
