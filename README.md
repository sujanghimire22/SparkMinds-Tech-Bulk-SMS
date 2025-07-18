# SparkMinds Tech Bulk SMS API Documentation

SparkMinds Tech provides a robust BULK SMS platform in Nepal, enabling seamless SMS communication across NTC and Ncell networks.

## Features of SparkMinds SMS

- Bulk SMS
- API Integration
- SMS Campaigns
- Interactive Messaging

## Bulk SMS

Send a high volume of SMS directly to mobile phones using our web-based or integrated platform. Perfect for alerts, promotions, or general communication.

## API SMS

Integrate SparkMinds SMS into your:

- Web apps
- CRMs
- ERPs
- Intranets and more

### API Endpoint

- **URL:** [https://sms.sparkminds.com.np/sms/v3/send](https://sms.sparkminds.com.np/sms/v3/send)
- **Method:** POST / GET
- **Parameters:** `auth_token`, `to`, `text`

| Field       | Type   | Description                               |
| ----------- | ------ | ----------------------------------------- |
| auth\_token | string | Client-specific token                     |
| to          | string | Comma-separated mobile numbers (10-digit) |
| text        | string | Message to be delivered                   |

### Sample Integrations

#### CURL

```bash
curl -s https://sms.sparkminds.com.np/sms/v3/send/ \
  -F auth_token='<your_token>' \
  -F to='98XXXXXXXX,98XXXXXXXX' \
  -F text='Hello from SparkMinds'
```

#### PHP

```php
$args = http_build_query([
  'auth_token' => '<your_token>',
  'to' => '98XXXXXXXX,98XXXXXXXX',
  'text' => 'Hello from SparkMinds'
]);

$ch = curl_init('https://sms.sparkminds.com.np/sms/v3/send/');
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_POSTFIELDS, $args);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$response = curl_exec($ch);
curl_close($ch);
```

#### Python

```python
import requests
r = requests.post('https://sms.sparkminds.com.np/sms/v3/send/', data={
  'auth_token': '<your_token>',
  'to': '98XXXXXXXX,98XXXXXXXX',
  'text': 'Hello from SparkMinds'
})
print(r.status_code, r.text)
```

## Advanced v4 Send (Multiple Recipients / Messages)

- **URL:** [https://sms.sparkminds.com.np/sms/v4/send-user](https://sms.sparkminds.com.np/sms/v4/send-user)
- **Method:** POST
- **Header:** `auth-token`
- **Body:** JSON with `to` and `text` arrays

### Example Body (Same Message)

```json
{
  "to": ["98XXXXXXXX", "98XXXXXXXX"],
  "text": ["Hello everyone"]
}
```

### Example Body (Different Messages)

```json
{
  "to": ["98XXXXXXXX", "98YYYYYYYY"],
  "text": ["Msg for X", "Msg for Y"]
}
```

## Credit Check

### Available Credit

- **URL:** [https://sms.sparkminds.com.np/sms/v4/available-credit](https://sms.sparkminds.com.np/sms/v4/available-credit)
- **Method:** GET
- **Header:** auth-token

### Full Credit Info

- **URL:** [https://sms.sparkminds.com.np/sms/v4/credit](https://sms.sparkminds.com.np/sms/v4/credit)
- **Method:** POST
- **Header:** auth-token

## Report API

- **URL:** [https://sms.sparkminds.com.np/sms/v4/api-report](https://sms.sparkminds.com.np/sms/v4/api-report)
- **Method:** POST
- **Parameters:** `start_date`, `end_date`
- **Header:** auth-token

## Interactive SMS

### Form Data

- **URL:** [https://sms.sparkminds.com.np/sms/v1/send/interactive-sms](https://sms.sparkminds.com.np/sms/v1/send/interactive-sms)
- **Method:** POST
- **Parameters:** `auth_token`, `campaign_id`, `to`, `text`

### JSON

- **URL:** [https://sms.sparkminds.com.np/sms/v1/send/interactive-sms-json](https://sms.sparkminds.com.np/sms/v1/send/interactive-sms-json)
- **Method:** POST
- **JSON Body:**

```json
{
  "auth_token": "<your_token>",
  "to": "98XXXXXXXX",
  "text": "Your message",
  "campaign_id": "123"
}
```

### Interactive SMS Report

- **URL:** [https://sms.sparkminds.com.np/sms/v1/report/interactive-sms](https://sms.sparkminds.com.np/sms/v1/report/interactive-sms)
- **Method:** POST
- **Parameters:** `auth_token`, `campaign_id`, `page`

## Contact

- **Email:** [enquiry@smtech.com.np](mailto\:enquiry@smtech.com.np)
- **Website:** [https://www.smtech.com.np](https://www.smtech.com.np)
- **Phone:** +977-97045150101
- **Address:** Bharatpur, Chitwan, Nepal

---
