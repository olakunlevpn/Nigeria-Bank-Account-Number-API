# Real-time Nigeria Bank Account validation API.
You can lookup any bank account details in Nigeria using our free bank API in few seconds to build applications faster and easy.


- Lifetime Access. Unlimited Account Lookups

- Enter account number and get the name and bank

- Enter account number and bank code to get the account name

- [Real-time Nigeria Bank Account Validation API Tutorial](https://maylancer.org/blog/real-time-nigeria-bank-account-validation-api-tutorial)


## Demo 
https://nubapi.com

## Documentation 
https://maylancer.org/docs/nuban/



## API Link
``` 
https://nubapi.com/verify?account_number={account_number}&bank_code={code}
```

Without bank code
``` 
https://nubapi.com/verify?account_number={account_number}
```



## Code Sample 
```php
/**
 * Makes an API call using cURL.
 *
 * @param string $method The HTTP method (POST, PUT, GET).
 * @param string $url The API URL.
 * @param mixed $data The data to be sent with the request.
 * @return mixed The API response.
 * @throws Exception If the cURL request fails.
 */
function callAPI($method, $url, $data) {
    $curl = curl_init();
 
    // Set cURL options based on the HTTP method
    switch ($method) {
        case "POST":
            curl_setopt($curl, CURLOPT_POST, 1);
            if ($data)
                curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
            break;
        case "PUT":
            curl_setopt($curl, CURLOPT_CUSTOMREQUEST, "PUT");
            if ($data)
                curl_setopt($curl, CURLOPT_POSTFIELDS, $data);
            break;
        default:
            if ($data)
                $url = sprintf("%s?%s", $url, http_build_query($data));
    }
 
    // Set common cURL options
    curl_setopt_array($curl, [
        CURLOPT_URL => $url,
        CURLOPT_HTTPHEADER => [
            'Content-Type: application/json',
            'Authorization: Bearer Your_Bearer_Token' // Replace with your actual Bearer token
        ],
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_HTTPAUTH => CURLAUTH_BASIC
    ]);
 
    // Execute the cURL request
    $result = curl_exec($curl);
 
    // Check for cURL errors
    if ($result === false) {
        $error = curl_error($curl);
        curl_close($curl);
        throw new Exception("cURL Request Failed: $error");
    }
 
    curl_close($curl);
 
    return $result;
}
 
// Define the API endpoint URL
$url = 'http://nubapi.com/api/verify';
 
// Set the API parameters
$params = [
    'account_number' => '12345678910',
    'bank_code' => '999992'
];
 
try {
    // Make the API call
    $get_data = callAPI('GET', $url, $params);
 
    // Decode the API response
    $response = json_decode($get_data, true);
 
    // Process the API response
    $data = [
        "firstname" => $response['first_name'],
        "lastname" => $response['last_name'],
        "othername" => $response['other_name'],
        "account_name" => $response['account_name'],
        "account_number" => $response['account_number'],
        "bank_name" => $response['Bank_name'],
        "status" => 'success'
    ];
 
    // Output the result as JSON
    echo json_encode($data, JSON_PRETTY_PRINT);
} catch (Exception $e) {
    // Handle cURL exceptions
    $errorMessage = $e->getMessage();
 
    $data = [
        "message" => "API Request Error: $errorMessage",
        "status" => 'error'
    ];
 
    echo json_encode($data, JSON_PRETTY_PRINT);
}

```


## Response JSON

```JSON
{
    "account_number": "123567890",
    "account_name": "CHIDUBEM IJENDU",
    "first_name": "CHIDUBEM",
    "last_name": "IJENDU",
    "other_name": "TIMOTHY",
    "Bank_name": "Bowen Microfinance Bank",
    "bank_code": "50931",
    "requests": "Free",
    "status": true
}
```


## Useful links 
  - Bank list html  https://nubapi.com/bank-html
  - Bank list Codes https://nubapi.com/bank
  - Bank list JSON  https://nubapi.com/bank-json
 

For support and inquiry Whatsapp Me https://wa.link/q1dmy4

## Legal
Its very legal & safe

## Security
Our API is highly secure and our system do not store any bank record


