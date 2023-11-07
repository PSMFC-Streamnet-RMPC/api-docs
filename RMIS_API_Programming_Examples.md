
# Interacting with the RMIS API

## Javascript Example
Get the first 10 location records where `reporting_agency` = `ODFW`

```javascript
const url = "https://phish.rmis.org/location";
const params = new URLSearchParams({
  page: 1,
  perpage: 10,
  reporting_agency: "ODFW"
});
const finalUrl = `${url}?${params}`;

const apiKey = "YOUR_API_KEY";
const headers = new Headers({
  "xapikey": `${apiKey}`
});

fetch(finalUrl, { headers })
  .then((response) => {
    if (response.ok) {
      return response.json();
    } else {
      throw new Error(`Error: ${response.status} ${response.statusText}`);
    }
  })
  .then((records) => {
    console.log("RMIS Location records retrieved:", records);
  })
  .catch((error) => {
    console.error(error);
  });
```

## Python Example
Get the first 10 location records where `reporting_agency` = `ODFW`

```python
import requests

url = "https://phish.rmis.org/location"
params = {
    'page': 1,
    'perpage': 10,
    'reporting_agency': "ODFW"
}
headers = {
    'x-api-key': "YOUR_API_KEY"
}

response = requests.get(url, params=params, headers=headers)

if response.ok:
    records = response.json()
    print("RMIS Location records retrieved:", records)
else:
    response.raise_for_status()  # This will raise an HTTPError if the HTTP request returned an unsuccessful status code.
```

## PHP Example
Get the first 10 location records where `reporting_agency` = `ODFW`

```php
$url = "https://phish.rmis.org/location";
$params = array(
    'page' => 1,
    'perpage' => 10,
    'reporting_agency' => 'ODFW'
);
$finalUrl = $url . '?' . http_build_query($params);

$apiKey = "YOUR_API_KEY";
$headers = array(
    "x-api-key: {$apiKey}"
);

$ch = curl_init($finalUrl);
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$response = curl_exec($ch);
$httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);

if ($httpCode == 200) {
    // Convert JSON to PHP array
    $records = json_decode($response, true);
    echo "RMIS Location records retrieved:";
    print_r($records);
} else {
    // Handle error, use curl_error($ch) to get the error message
    echo "Error: " . $httpCode . curl_error($ch);
}

curl_close($ch);
```

## Visual Basic Example
Get the first 10 location records where `reporting_agency` = `ODFW`

```vbnet
Imports System.Net.Http
Imports System.Text.Json
Imports System.Threading.Tasks

Module Module1
    Sub Main()
        ' Start the asynchronous operation
        MainAsync().GetAwaiter().GetResult()
    End Sub

    Async Function MainAsync() As Task
        
        Dim baseUrl As String = "https://phish.rmis.org/location"
        Dim apiKey As String = "YOUR_API_KEY"
        Dim client As HttpClient = New HttpClient()

        ' Set up the request headers
        client.DefaultRequestHeaders.Add("x-api-key", apiKey)

        ' Set up the query parameters
        Dim queryParams As New Dictionary(Of String, String) From {
            {"page", "1"},
            {"perpage", "10"},
            {"reporting_agency", "ODFW"}
        }

        ' Create the URL with query parameters
        Dim finalUrl As String = $"{baseUrl}?{String.Join("&", queryParams.Select(Function(kvp) $"{kvp.Key}={kvp.Value}"))}"

        Try
            ' Send the GET request
            Dim response As HttpResponseMessage = Await client.GetAsync(finalUrl)
            If response.IsSuccessStatusCode Then
                ' Read the response as a JSON object
                Dim jsonContent As String = Await response.Content.ReadAsStringAsync()
                Dim records As JsonElement = JsonDocument.Parse(jsonContent).RootElement
                Console.WriteLine("RMIS Location records retrieved: " & records.ToString())
            Else
                Console.WriteLine($"Error: {response.StatusCode} {response.ReasonPhrase}")
            End If
        Catch ex As Exception
            Console.WriteLine("Exception occurred: " & ex.Message)
        Finally
            ' Clean up the HttpClient
            client.Dispose()
        End Try
    End Function
End Module
```
