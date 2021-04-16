# Nigeria-Bank-Account-Number-API for free 
You can use it to get the account name of any bank account in Nigeria


- Lifetime Access. Unlimited Account Lookups

- Enter account number and get the name and bank

- Enter account number and bank code to get the account name

## Demo 
https://maylancer.org/api/nuban/

## API Link
``` 
https://maylancer.org/api/nuban/api.php?account_number={account_number}&bank_code={code}
```

Without bank code
``` 
https://maylancer.org/api/nuban/api.php?account_number={account_number}
```


## Response JSON

``` 
{
    "account_number": "0080******",
    "account_name": "Jane Doe",
    "Bank_name": "ACCESS BANK PLC",
    "bank_code": "044",
    "requests": "Free",
    "execution_time": "0.17 secs",
    "status": "success"
}
```

## Code Sample 
```
function callAPI($method, $url, $data){
   $curl = curl_init();
   switch ($method){
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
   // OPTIONS:
   curl_setopt($curl, CURLOPT_URL, $url);
   curl_setopt($curl, CURLOPT_HTTPHEADER, array(
      'Content-Type: application/json',
   ));
   curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
   curl_setopt($curl, CURLOPT_HTTPAUTH, CURLAUTH_BASIC);
   // EXECUTE:
   $result = curl_exec($curl);
   if(!$result){die("Connection Failure");}
   curl_close($curl);
   return $result;
}



$get_data = callAPI('GET', 'https://maylancer.org/api/nuban/api.php?account_number={account_number}&bank_code={code}', false);
$response = json_decode($get_data, true);




if (isset($response['account_name'])) {


	$name = explode(' ', $response['account_name']);

    $length=count($name);
	//create array
    $data = array(
    	"firstname" => $name[0],
    	"lastname" => $name[$length-1],
        "account_name" => $response['account_name'],
        "account_number" => $response['account_number'],
        "bank_name" => $response['Bank_name'],
        "status" => 'success'
        
    );
}else{

	$data = array(
        "message" => 'Invalid account number entered, '.$response['message'],
        "status" => 'error'
        
    );
}





echo json_encode($data, JSON_PRETTY_PRINT);

```

## Useful links 
  - Bank list html  https://maylancer.org/api/nuban/banklist.php?type=html
  - Bank list Codes https://maylancer.org/api/nuban/banklist.php?type=bank_code
  - Bank list JSON  https://maylancer.org/api/nuban/banklist.php
 

For support and inquiry Whatsapp Me https://wa.link/q1dmy4

## Legal
Its very legal & safe

## Security
Our API is higly secure and our system do not store any bank record

You can use the hosted version freely, if you want the source code kindly whatsapp me to get it for free https://wa.link/zi3b0k
