# payment result query
## Description
Merchants can call this API from server-side to obtain the information on a particular transaction, such as the pay_result, dt_order, money_order, settle_date, info_order, etc. 
###### Endpoint

```html
https://wallet.lianlianpay.com/llwalletapi/orderquery.htm
```

###### Request Parameters

  <table>
   <tr>
      <td>Name</td>
      <td>Required</td>
      <td>Type(length)</td>
      <td>Description and Example</td>
   </tr>
   <tr>
      <td colspan="4">Basic Parameters</td>
   </tr>
   <tr>
      <td>oid_partner</td>
      <td>Y</td>
      <td>String(18)</td>
      <td>A unique 18 digit number to identify a contracted merchant account. . e.g. 201304121000001004</td>
   </tr>
   <tr>
      <td>sign_type</td>
      <td>Y</td>
      <td>String(3)</td>
      <td>RSA</td>
   </tr>
   <tr>
      <td>sign</td>
      <td>Y</td>
      <td>String</td>
      <td>Signature value</td>
   </tr>
   <tr>
      <td colspan="4">Business Parameters</td>

   </tr>
   <tr>
      <td>no_order</td>
      <td>N</td>
      <td>String(32)</td>
      <td>Merchant order No.It's an either-or choice between no_order and oid_paybill.</td>
   </tr>
   <tr>
      <td>dt_order</td>
      <td>N</td>
      <td>String(14)</td>
      <td>Merchant order date. Format: YYYYMMDDHHMMSS, e.g. 20170801225714</td>
   </tr>
   <tr>
      <td>oid_paybill</td>
      <td>N</td>
      <td>String(14)</td>
      <td>The unique trade number in lianlian Pay system.</td>
   </tr>
   <tr>
      <td>type_dc</td>
      <td>Y</td>
      <td>String(1)</td>
      <td class="AutoNewline">transaction type
        
    0:merchant collect money
    1:payment from merchant（merchant withdraw,）
    2:user collect money(collect money,transfer account and recharge)
    3:user withdraw</td>
   </tr>
   <tr>
      <td>query_version</td>
      <td>N</td>
      <td>String(6)</td>
      <td>The query API version.The default is 1.0</td>
   </tr>
   <tr>
      <td>user_id</td>
      <td>N</td>
      <td>String(32)</td>
      <td>The unique identification assigned to the user in the merchant’s system</td>
   </tr>

</table>

method : POST <br>
format : JSON
###### Sample Request


```html
{ "oid_partner":"201103171000000000", "dt_order":"20130515094013", "no_order":"2013051500001", "sign_type ":"RSA", "sign":"ZPZULntRpJwFmGNIVKwjLEF2Tze7bqs60rxQ22CqT5J1UlvGo575QK9z/+p+7E9cOoRoWzqR6xHZ6WVv3dloyGKDR0btvrdqPgUAoeaX/YOWzTh00vwcQ+HBtXE+vPTfAqjCTxiiSJEOY7ATCF1q7iP3sfQxhS0nDUug1LP3OLk=" }

```


## Sync Response


###### Parameters

|Name|Required|Type|Description|
|---|---|---|---|
|ret_code|Y|String(4)|0000|
|ret_msg|Y|String(100)|Return message, description of ```ret_code```, in Chinese e.g.交易成功|
|sign_type|Y|String(3)|RSA |
|sign|Y|String|Signature value|
|result_pay|Y|String| Payment result<br>SUCCESS<br>PROCESSING<br>WAITING<br>FAILURE|
|oid_partner|Y|String(18)|A unique 18 digit number to identify a contracted merchant account. . e.g. 201304121000001004|
|dt_order|Y|String(14)|Merchant order date. Format: YYYYMMDDHHMMSS, e.g. 20170801225714|
|no_order|Y|String(32)|Merchant order No.|
|oid_paybill|Y|String(18)|Unique transaction No. in LianLian system. e.g. 2011030900001098|
|money_order|Y|String(12)|Merchant order amount, range: 0.01 ~ 100,000,000.00, 2 decimal places are expected, in CNY|
|settle_date|N|String(8)| Format YYYYMMDD. Returns when payment is successful|
|info_order|N|String(255)| Returns when ```info_order``` is sent in API requests|
|bank_code|N|String| |
|bank_name|N|String| |
|memo|N|String| |
|pay_type|N|String| |
###### Sample 
{ "oid_partner":"201103171000000000", "dt_order":"20130515094013", "no_order":"2013051500001", "result_pay":"SUCCESS", "oid_paybill":"2013051500001", "money_order":"49.65", "settle_date":"20130515", "info_order":"用户13958069593购买了3桶羽毛球", "pay_type":"2", "bank_code":"01020000", "sign_type ":"RSA", "sign":"ZPZULntRpJwFmGNIVKwjLEF2Tze7bqs60rxQ22CqT5J1UlvGo575QK9z/+p+7E9cOoRoWzqR6xHZ6WVv3dloyGKDR0btvrdqPgUAoeaX/YOWzTh00vwcQ+HBtXE+vPTfAqjCTxiiSJEOY7ATCF1q7iP3sfQxhS0nDUug1LP3OLk=" }


