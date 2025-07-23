# SparkMinds Tech Bulk SMS API Documentation

SparkMinds Tech provides a robust BULK SMS service in Nepal, enabling seamless SMS communication across NTC and Ncell networks.

## Features of SparkMinds SMS

- Bulk SMS
- API Integration
- SMS Campaigns
- Interactive Messaging


## 📦 BULK SMS

Bulk Messaging allows mass dissemination of SMS directly to mobile numbers from your application or dashboard.
Typical use cases:
- Alerts & Notifications
- Marketing Campaigns
- Reminders & Promotions



### API SMS ###

Our APIs enable customers to seamlessly integrate SMS functionality into every aspect of their business systems — including applications, websites, intranets, CRMs, ERPs, and other enterprise software — delivering real-time messaging capabilities within their existing platforms.

* Url: https://sms.sparkminds.com.np/sms/v3/send
* Parameter: auth_token,to,text
* Method: POST / GET

| Field     | Type   | Description                             |
| ----------|:------:| -----:                                  |
| auth_token| string | Token generated from our website.       |
| to        | string | Comma Separated 10-digit mobile numbers.|
| text      | string | SMS Message to be sent.                 |



## Also find the examples for API Integration below : ##

### API - Examples using POST method  ###

#### CURL ####

```curl

curl -s https://sms.sparkminds.com.np/sms/v3/send/ \
    -F token='<token from dashboard>' \
    -F to='<comma separated 10 digits mobile numbers>' \
    -F text='<message to be sent>'

```

#### PHP ####

```php
	
	$args = http_build_query(array(
	        'auth_token'=> '<token from dashboard>',
	        'to'    => '<comma separated 10 digits mobile numbers>',
	        'text'  => '<message to be sent>'));
	$url = "https://sms.sparkminds.com.np/sms/v3/send/";

	# Make the call using API.
	$ch = curl_init();
	curl_setopt($ch, CURLOPT_URL, $url);
	curl_setopt($ch, CURLOPT_POST, 1); ///
	curl_setopt($ch, CURLOPT_POSTFIELDS,$args);
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1); 
	// Response
	$response = curl_exec($ch);
	curl_close($ch);			

```

#### PYTHON ####

```python

	import requests
	r = requests.post(
	        "https://sms.sparkminds.com.np/sms/v3/send/",
	        data={ auth_token: '<token from dashboard>',
	              'to'      : '<comma separated 10 digits mobile numbers>',
	              'text'    : '<message to be sent>'})
	status_code = r.status_code
	response = r.text
	response_json = r.json()

```

#### C# (C-sharp) ####

```Csharp

using System.Collections.Specialized;
using System.Net;
using System.Text;

namespace PostSMS{

    class Program{

        static void Main(string[] args){
                var responseTest = SendSMS('<token from dashboard>', '<comma separated 10 digits mobile numbers>', '<message to be sent>');
        }

        private static string SendSMS(string token, string to, string text){

            using (var client = new WebClient()){
                var values = new NameValueCollection();
                values["auth_token"] = token;
                values["to"] = to;
                values["text"] = text;
                var response = client.UploadValues( "https://sms.sparkminds.com.np/sms/v3/send/",  "Post", values);
                var responseString = Encoding.Default.GetString(response);
                return responseString;
            }
        }
    }
}

```

### Success Response

```
{
    "error": false,
    "message": "1 messages has been queued for delivery.",
    "data": {
        "valid": [
            {
                "id": 2673160,
                "mobile": "9779818000000",
                "text": "v3 sms test",
                "credit": 1,
                "network": "ncell",
                "status": "queued"
            }
        ],
        "invalid": [
            {
                "mobile": "988585584",
                "text": "v3 sms test",
                "credit": 0,
                "network": "N/A",
                "status": "aborted"
            }
        ]
    }
}

```

### Failure Response

```
# if auth token is invalid. 
{
    "error": true,
    "message": "The provided Auth Token is not valid.",
    "data": []
}

# if auth token field is missing.
{
    "error": true,
    "message": "The auth token field is required.",
    "data": []
}

# if to field is missing.
{
    "error": true,
    "message": "The to field is required.",
    "data": []
}

# if text field is missing.
{
    "error": true,
    "message": "The text field is required.",
    "data": []
}

# if credit is not enough.
{
    "error": true,
    "message": "Not enough balance.",
    "data": []
}
```


### Send SMS to Multiple Numbers ###

You can now send a single message to multiple recipients or send different messages to multiple recipients using this API. The **to** and **text** fields accept arrays, offering greater flexibility. By passing an array of phone numbers in the **to** field and corresponding messages in the **text** field, you can efficiently send one message to many users or tailor individual messages for each recipient.


* Url: https://sms.sparkminds.com.np/sms/v4/send-user
* Header Parameter: auth-token
* Body Parameters: to,text
* Method: POST


 Field     | Type   | Description                             |
| ----------|:------:| -----:                                  |
| auth-token| string | Token generated from our website.       |
| to        | array | Array of recipient phone numbers.|
| text      | array | Array of SMS messages corresponding to each number.|

## Request Format ##
Query Parameter:

auth-token: Token generated from our website.

ex: https://sms.sparkminds.com.np/sms/v4/send-user

Body Parameters:

To send the same SMS message to multiple recipients:
```
{
    "to": [
        "98XXXXXXXX",
        "98XXXXXXXX",
    ],
    "text": [
        "Hello world"
    ]
}
```

To send different messages to each recipient:
```
{
    "to": [
        "98XXXXXXXX",
        "98XXXXXXXX",
    ],
    "text": [
        "Hello world 1"
        "Hello world 2"
    ]
}
```


## Also find the examples for API Integration below : ##

### API - Examples using POST method  ###

#### PHP ####

```
$url = 'https://sms.sparkminds.com.np/sms/v4/send-user';
$auth-token = 'your_auth_token_here';  // Replace with your auth token

$data = [
    'to' => ['98XXXXXXXX', '98XXXXXXXX'],  // Phone numbers
    'text' => ['Hello world']              // SMS text
];


// Initialize cURL and set optionsx
$ch = curl_init($url);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
$headers = [
    'auth-token: ' . $auth_token
];
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($data));

$response = curl_exec($ch);
curl_close($ch);

```

### Success Response

```
{
    "responses": [
        {
            "error": false,
            "message": "1 messages have been queued for delivery.",
            "data": {
                "valid": [
                    {
                        "id": "8967_173191065276114",
                        "mobile": "977XXXXXXXXXXX",
                        "text": "test test",
                        "credit": 1,
                        "network": "ntc",
                        "status": "queued",
                        "shortcode": "XXXXXXXX"
                    }
                ],
                "invalid": []
            }
        }
    ],
    "errors": []
}


```

## Failure Response ##

```
# if phone number are incorrect. 

{
    "error": true,
    "message": "All messages encountered errors.",
    "errors": [
        {
            "error": true,
            "message": "No valid recipients.",
            "data": {
                "valid": [],
                "invalid": [
                    {
                        "mobile": "98XXXXXX",
                        "text": "test test",
                        "credit": 0,
                        "network": "N/A",
                        "status": "aborted",
                        "shortcode": ""
                    }
                ]
            }
        }
    ]
}
# if auth token is invalid. 
{
    "error": true,
    "message": "The provided Auth Token is not valid.",
    "data": []
}

# if auth token field is missing.
{
    "error": true,
    "message": "The auth token field is required.",
    "data": []
}

# if to field is missing.
{
    "error": true,
    "message": "The to field is required.",
    "data": []
}

# if text field is missing.
{
    "error": true,
    "message": "The text field is required.",
    "data": []
}

# if credit is not enough.

{
    "error": true,
    "message": "All messages encountered errors.",
    "errors": [
        {
            "error": true,
            "message": "Not enough balance.",
            "data": []
        }
    ]
}


```



## Credit with Total Sms check ##

* URL :: https://sms.sparkminds.com.np/sms/v4/credit
* Http Request : POST
* In header : auth-token   (Your Api Token Value)

| Header     | Value   | Description                             |
| ----------|:------:| -----:                                  |
| auth-token| string | Token generated from our website.       |


#### Responses ####

```
{

    available_credit: xxx,
    "total_sms_sent" : xxx,
    last_transaction_date : xxx,
    "last_transaction_date_sms_sent" : xxx
    response_code: 202

}

```


## Only Available Credit check ##

* URL :: https://sms.sparkminds.com.np/sms/v4/available-credit
* Http Request : GET
* In header : auth-token   (Your Api Token Value)

| Header     | Value   | Description                             |
| ----------|:------:| -----:                                  |
| auth-token| string | Token generated from our website.       |


#### Responses ####

```
{

    available_credit: xxx,
    response_code: 200

}

```


### Report API SMS


* URL: https://sms.sparkminds.com.np/sms/v4/api-report
* Method: POST
* Parameters: start_date, end_date
* Header: auth-token (Token generated from our website)

| Field     | Type    | Description                             |
| ----------|:------: | -----:                                  |
| start_date| date  | Y-m-d (Ex.2025-01-01)                     |
| end_date  | date  | Y-m-d (Ex.2025-01-30) 


OR

* URL: https://sms.sparkminds.com.np/sms/v1/report/api 
* Method: POST
* Parameters: auth_token, page

| Field     | Type    | Description                             |
| ----------|:------: | -----:                                  |
| auth_token| string  | Token generated from our website.       |
| page      | integer | Start from 1,2......


### Pull/Incoming API 

* URL: Public URL where the incoming SMS has to be forwarded.
* Method: GET

GET request is sent to the URL provided with following arguments:


| Field       | Description                             |
| ----------- | -----:                                  |
| keyword     | Get your Keyword                        |
| from        | Mobile number from where message coming |
| text        | Message send by user to your campaign (example: keyword + other text)   |


### Pull/Incoming Custom Campaign API 

* URL: Public URL where the incoming SMS has to be forwarded and get response from your end as a reply message to user.
* Method: GET

GET request is sent to the URL provided with following arguments:


| Field       | Description                             |
| ----------- | -----:                                  |
| keyword     | Get your Keyword                        |
| from        | Mobile number from where message coming |
| text        | Message send by user to your campaign (example: keyword + other text)   |

#### Response 

You need to implement logic to handle incoming requests and respond with a text message (maximum 160 characters) along with a response code. If any response code other than the expected one is returned, a default SMS reply will be automatically sent to the user.


```
{"success":True,"message":"Your Custom Auto reply Message"}

```

| Field       | Description                             |
| ----------- | -----:                                  |
| success       | True/False                              |
| message     | Your Custom Auto reply Message         |



### SMS Campaign ###

You can create individual campaigns to generate leads for your products and services. This allows you to collect valuable data on potential customers who are most likely to be interested in what you offer.

* Voting
* Poll
* Quize
* Instant

### SMS Voting ###

SMS Polls offer a quick and effective way to gauge your audience’s opinions. With a simple text message, you can launch an interactive mobile poll that keeps your audience engaged while delivering valuable insights for your business.

## Interactive SMS


### 1. Send Interactive SMS using Form-Data

* URL: https://sms.sparkminds.com.np/sms/v1/send/interactive-sms 
* Method: POST
* Parameters: auth_token, campaign_id, text, to

| Field      | Type    | Description                             |
| ---------- |:------: | -----:                                  |
| auth_token | string  | Token generated from our website.       |
| campaign_id| integer | Get from dashboard                      |
| to         | string  | Comma Separated 10-digit mobile numbers.|
| text       | string  | SMS Message to be sent.                 |


## Also find the examples for Interactive API Integration below : ##

### Interactive API - Examples using POST method  ###

#### PHP ####

```php

$post = [
    'auth_token'=> '<token from dashboard>',
    'campaign_id'  => 'get from dashboard',
    'to'    => '<comma separated 10 digits mobile numbers>',
    'text'  => '<message to be sent>'
];

$ch = curl_init('https://sms.sparkminds.com.np/sms/v1/send/interactive-sms');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, $post);

// execute!
$response = curl_exec($ch);

// close the connection, release resources used
curl_close($ch);

```

### 2. Send Interactive SMS using JSON

* URL: https://sms.sparkminds.com.np/sms/v1/send/interactive-sms-json  
* Method: POST
* Request: 

`````
{

    "auth_token": "YOUR AUTH TOKEN",
    "to": "COMMA SEPARATED MOBILE NUMBER",
    "text": "MESSAGE YOU WANT TO SEND",
    "campaign_id": "YOU GET THIS NUMBER AFTER YOU CREATE CAMPAIGN FROM DASHBOARD"
}

`````

### 3. Report - Interactive SMS

* URL: https://sms.sparkminds.com.np/sms/v1/report/interactive-sms  
* Method: POST
* Parameters: auth_token, campaign_id, page

| Field      | Type    | Description                             |
| ---------- |:------: | -----:                                  |
| auth_token | string  | Token generated from our website.       |
| campaign_id| integer | Get from dashboard                      |
| page       | integer | Start from 1,2...                       |

### Interactive API Report - Examples using POST method  ###

#### PHP ####

```php

$post = [
    'auth_token'=> '<token from dashboard>',
    'campaign_id'  => 'get from dashboard',
    'page'    => '<start from 1>'
];

$ch = curl_init('https://sms.sparkminds.com.np/sms/v1/report/interactive-sms');
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, $post);

// execute!
$response = curl_exec($ch);

// close the connection, release resources used
curl_close($ch);

```
## Contact

- **Email:** [enquiry@smtech.com.np](mailto\:enquiry@smtech.com.np)
<strong>Website:</strong> <a href="https://www.smtech.com.np" target="_blank" rel="noopener noreferrer">https://www.smtech.com.np</a>
- **Phone:** +977-97045150101
- **Address:** Bharatpur, Chitwan, Nepal

---
