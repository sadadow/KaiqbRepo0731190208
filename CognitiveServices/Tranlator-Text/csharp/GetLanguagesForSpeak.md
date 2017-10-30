## Get supported languages for speech synthesis

The following code gets a list of language codes representing languages supported for speech synthesis, using the GetLanguagesForSpeak method.

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
        static string path = "/V2/Http.svc/GetLanguagesForSpeak";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        async static void GetLanguagesForSpeak()
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
            GetLanguagesForSpeak();
            Console.ReadLine();
        }
    }
}
```

**Get supported languages for speech synthesis response**

A successful response is returned in XML, as shown in the following example: 

```xml
<ArrayOfstring xmlns="http://schemas.microsoft.com/2003/10/Serialization/Arrays" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <string>ar</string>
  <string>ar-eg</string>
  <string>ca</string>
  <string>ca-es</string>
  <string>da</string>
  <string>da-dk</string>
  <string>de</string>
  <string>de-de</string>
  <string>en</string>
  <string>en-au</string>
  <string>en-ca</string>
  <string>en-gb</string>
  <string>en-in</string>
  <string>en-us</string>
  <string>es</string>
  <string>es-es</string>
  <string>es-mx</string>
  <string>fi</string>
  <string>fi-fi</string>
  <string>fr</string>
  <string>fr-ca</string>
  <string>fr-fr</string>
  <string>hi</string>
  <string>hi-in</string>
  <string>it</string>
  <string>it-it</string>
  <string>ja</string>
  <string>ja-jp</string>
  <string>ko</string>
  <string>ko-kr</string>
  <string>nb-no</string>
  <string>nl</string>
  <string>nl-nl</string>
  <string>no</string>
  <string>pl</string>
  <string>pl-pl</string>
  <string>pt</string>
  <string>pt-br</string>
  <string>pt-pt</string>
  <string>ru</string>
  <string>ru-ru</string>
  <string>sv</string>
  <string>sv-se</string>
  <string>yue</string>
  <string>zh-chs</string>
  <string>zh-cht</string>
  <string>zh-cn</string>
  <string>zh-hk</string>
  <string>zh-tw</string>
</ArrayOfstring>
```
