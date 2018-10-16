# FlashPay

>## API URL

    test URL：https://paychanneldev.pagsmile.com:8443/api/flashpay
    prod URL：https://paychannel.pagsmile.com/api/flashpay 
    
>## Request Method

     POST

>## Format
  
    json
    
>## Parameters

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Merchant_no | String | Yes | 20 | pagsmile assigned to the merchant's ID | 1024201708140012289
App_id | String | Yes | 20 | pagsmile application ID assigned to the merchant | 2017051914172236111
Version | String | Yes | 10 | The version of the interface being called, fixed at: 1.0 | 1.0
Timeout_express | String | Yes | 255 | Order Validity | The time of day is assigned: 1d or 24h or 1440m;
Passback_params | String | Yes | 255 | Transparent pass parameters | default passback_params
Timestamp | String | Yes | 19 | Time to send request in seconds | 21516081919
Sign_type | String | Yes | 10 | Currently only supports MD5 | MD5
Payment.out_order_no | String | Yes | 64 | Merchant Order Number |
Payment.order_amount | String | Yes | 10 | The total amount of the order, accurate to two decimal places. | 88.88
Payment.currency | String | Yes | 3 | Currency | BRL
Payment.method | String | Yes | 10 | Channel Code (default) | 110010
Payment.subject | String | No | 255 | Order Title |
Payment.content | String | No | 255 | Order Content |
Payment.bank | String | Yes | 255 | Payment Bank |tau, santander, bradesco, banco-do-brasil
Payment.notify_url | String | Yes | 255 | The server actively notifies the http/https path of the page specified in the merchant server. | https://www.pagsmile.com
Customer.out_uid | String | No | 255 | Merchant User ID |
Customer.email | String | Yes | 255 | Email Address |
Customer.cpf_no | String | Yes | 64 | CPF Number |
Customer.username | String | Yes | 255 | User Name |
Customer.buyer_ip | String | No | 255 | Merchant ipv4 address |
Customer.browser | String | No | 255 | User's browser type |
Customer.phone | String | Yes | 9 | Phone of the merchant's user, 8 or 9 digits |
Sign | String | Yes | 32 | Signature string of merchant request parameters | Signature value calculated by signature algorithm, see signature generation algorithm

     Note: The currency currently only supports USD and BRL, which is used in the test environment.
     
        Cpf_no and username are 50284414727 and Test User Name
    
     Payment bank parameters currently support four banks namely itau, santander, bradesco, banco-do-brasil

>## Request Sample

```
    {
        "merchant_no":"102320170519",
        "app_id":"2017051914172236111",
        "timestamp":1516187084,
        "version":"1.0",
        "timeout_express":"15d",
        "passback_params":"passback_params",
        "sign_type":"md5",
        "payment":{
                    "out_order_no":"test-003192",
                    "order_amount":10,
                    "method":"110010",
                    "currency":"BRL",
                    "subject":"test-subject",
                    "content":"test-content",  
                    "bank":"itau",            
                    "notify_url":"www.pagsmile.com",  
                   },
        "customer":{
                    "username":"Test User Name",
                    "buyer_ip":"127.0.0.1",
                    "browser":"safari",
                    "email":"test@pagsmile.com",
                    "cpf_no":"50284414727",
                    "out_uid":"out_uid",
                    "phone":"941523675"
                    },
        "address":{
                    "zip_code":"06233-200",
                    "street_name":"Av. das Nações Unidas",
                    "street_number":"3003",
                    "neighborhood":"Bonfim",
                    "city":"Osasco",
                    "federal_unit":"SP"
                    },               
        "sign":"c7412c2458a135dd3d37a655ef796a41"
    }

``` 

>## Return

After the request is successful, the returned data is in info. The returned data is returned in json format.

Parameter | Type | Required | Maximum length | Description | Example value
--- | --- | --- | --- | --- | ---
Code | String | Yes | 16 | Return to status code (success is 200) | 200
Info.trade_no | String | Yes | 128 | Platform Order Number | 2017042311015505011
Info.out_order_no | String | Yes | 128 | Merchant Order Number | test-003192
Info.total_amount | float | Yes | 10 | Order Amount | 10
Info.bank_name | String | Yes | 10 | Payment to Public Account Name Bank Name |
Info.account_owner | String | Yes | 50 | Payment to Public Account Name |
Info.account_owner_document | String | Yes | 10 | Payment to public account cpf number |
Info.account_agency | String | Yes | 10 | Bank Branch Number |
Info.account_number | String | Yes | 10 | Bank account |
Info.bank_logo | String | Yes | 10 | Bank logo |
Info.check_url | String | Yes | 10 | Payment voucher verification link |

>## Success Sample

```
    { 
    "code":"200",
    "info":{"code":"200","info":{"trade_no":"2018070909341506645","currency":"USD","amount":100,"bank_name":itau,"out_order_no":"test-0011531140105503","account_owner":"Agillitas Solu","account_owner_document":"13.776.742\/0001-55","account_agency":"0910","account_number":"05841-1","bank_logo":"https:\/\/d2g83ydku1zde9.cloudfront.net\/pagsmile\/Itau-logo.png","check_url":"http:\/\/bit.ly\/2NFMlMK"}
    
```

>## Fail Sample

```
    { 
    "code":"403",
    "info":"SIGN_ISNULL"
    }
    
```  

>## Error Code

For a more detailed list, please refer to [Return Status and Error List](ReturnResult)

>## Signature Generation Algorithm

Reference [Direct Connection Signature Algorithm](DriectSign)