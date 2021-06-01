---
title: Exchange-official-API-docs

language_tabs: # must be one of https://git.io/vQNgJ
  

toc_footers:

includes:
  
language: English

other_language: 简体中文

url: /cn

present_url: /en

active: active

other_active:

menu: Menu

spot_goods: Exchange 

spot_goods_active: active


searchText: Search

search: true

code_clipboard: true
---



# Introduction

## <span>API Introduction</span>


Welcome to CoinW API！

This is the official CoinW API document, and will be continue updating, please follow us to get latest news.

You can switch to different API business in the top menu, and switch to different language by clicking the button in the top right.

The example of request and response is showing in the right hand side.

## <span>Description</span>

1.Get API authenticated api key and secret key

You canget api key and secret key by applying for API, and api key is the access key provided to API users, secret key is used to sign the request parameters. Warning: These two keys are important to your account safety, please don't share both of them together to anyone else.

2.Generate to be signed string

All parameters submitted by the user, except sign, must participate in the signature. The string to be signed needs to be sorted according to the parameter name (all parameter names are arranged in abcd order according to their first letters firstly, and if the same first letter is encountered, then the second letter, and so on.) For example: For the following The parameters are signed string [] parameters = {"api_key = c821db84-6fbd-11e4-a9e3-c86000d26d7c", "symbol = btc_cny" type = 0 "price = 680" amount = 1.0 "}; The string to be signed is: amount = 1.0 & api_key = c821db84-6fbd-11e4-a9e3-c86000d26d7c & price = 680 & symbol = btc_cny & type = 0

3.MD5 Signature

When signing MD5, the secret key is required to participate in the signature. Add the secret key parameter to the signature string to generate the final signature string, for example: amount = 1.0 & api_key = c821db84-6fbd-11e4-a9e3-c86000d26d7c & price = 680 & symbol = btc_cny & type = 0 & secret_key = secretKey Note that "& secret_key = secretKey" is signature required parameter. A 32-bit MD5 algorithm is used to perform a signature operation on the final signature string to be signed to obtain a signature result string (the string is assigned to the parameter sign). All letters in the MD5 calculation result are capitalized.

## <span>Contact Us</span>

If you have any other questions on API, you can contact us by below ways:

·Join official QQ group (967798979), please tell your UID and programming language in your join request.

# Basic API

## <span>Get trading pair summary information</span>


Get the basic information of the trading market of CoinW. 

The symbol parameters used by other API interfaces are obtained from here, so before using other APIs, please obtain the necessary information through this API.

Retrieve summary information for each currency pair listed on the exchange

**HTTP Request**

> GET /api/v1/public?command=returnTicker

`curl "http://api.coinw.fm/api/v1/public?command=returnTicker"`

Request Parameters

No parameter is needed for this endpoint.

Response Content

Field	 | Data Type	 | Description
-------------- | -------------- | --------------
id	 | string | 	id
last | 	string | 	Latest price
lowestAsk | 	string | 	Lowest sale
highestBid	 | string	 | Highest buy
percentChange	 | string | 	Change
isFrozen | 	string | 	Lock or not
high24hr | 	string	 | High 24H
low24hr | 	string | 	Low price
baseVolume	 | string	 | Base currency volume 24H


```json

                {
                    "code":"200",
                    "data":{
                        "EET_CNYT":{
                            "percentChange":"0",
                            "high24hr":"0.0",
                            "last":"0.008",
                            "highestBid":"0.007",
                            "id":39,
                            "isFrozen":0
                            "baseVolume":"0.0",
                            "lowestAsk":"0.008",
                            "low24hr":"0.0"
                        }
                    },
                    "msg":"SUCCESS"
                }
    
```       

## <span>Currency information</span>


Back to currency related info

**HTTP Request**

> GET/api/v1/public?command=returnCurrencies

`curl "https://api.coinw.fm/api/v1/public?command=returnCurrencies"`

Request Parameters

No parameter is needed for this endpoint.

Response Content

Field	| Data Type	| Description
-------------- | -------------- | --------------
maxQty	| string| 	Max Withdrawal
minQty	| string	| Min Withdrawal
recharge	| string	| Whether it can be deposited, 0 cannot 1 can
symbol| 	string	| Currency
symbolId	| string	| Symbol
txFee| 	string	| Fee
withDraw	| string	| Whether it can be withdrawn, 0 cannot 1 can


```json
            {
                "code":"200",
                "data":{
                    "HC":{
                        "maxQty":"1000000.0",
                        "minQty":"10.0",
                        "recharge":"1",
                        "symbol":"HC",
                        "symbolId":"6",
                        "txFee":"0.0",
                        "withDraw":"1"
                    },
                    "LEEK":{
                        "maxQty":"999999.0",
                        "minQty":"1000.0",
                        "recharge":"1",
                        "symbol":"LEEK",
                        "symbolId":"55",
                        "txFee":"0.0",
                        "withDraw":"1"
                    },"XMR":{
                        "maxQty":"1000.0",
                        "minQty":"0.1",
                        "recharge":"1",
                        "symbol":"XMR",
                        "symbolId":"88",
                        "txFee":"0.0",
                        "withDraw":"1"
                    },"GLA":{
                        "maxQty":"9.99999999E8",
                        "minQty":"100.0",
                        "recharge":"0",
                        "symbol":"GLA",
                        "symbolId":"39",
                        "txFee":"0.0",
                        "withDraw":"0"
                        }
                    },
                    "msg":"SUCCESS"
                }
        
```

# Market API

Get current market data

## <span>Get depth</span>

Get depth

Back to the trading pair depth info

**HTTP Request**
> GET /api/v1/public?command=returnOrderBook

`curl
"https://api.coinw.fm/api/v1/public?command=returnOrderBook&symbol=BTC_CNYT&size=20"`

Request Parameters

Field | DataType |must |Defaults | Description
-------------- | -------------- | --------------| --------------| --------------
size|	Int	|  false | 5|	Depth | value |（5，20）
symbol	|  string  | true	|	 | Trading pair like: BTC-CNYT
Response Content

Field|Data Type|Description
-------------- | -------------- | --------------
asks	|string|	Buyer'sdepth
bids	|string|	Seller's depth

```json
                  {
                      "code":"200",
                      "data":{
                          "asks":[
                              ["3.263","0.01"],
                              ["7.90",0.01],
                              ["8.00","20.55"],
                              ["8.177","51.25"],
                              ["8.287","202.05"]
                          ],
                          "bids":[
                              ["3.262","302.00"],
                              ["3.261","233.10"],
                              ["3.26","34.00"],
                              ["3.259","416.90"],
                              ["3.258","113.50"]
                          ]
                      },
                      "msg":"SUCCESS"
                  }
      
```
        
## <span>Latest trading pair</span>

Back to the trading pair's last 200 trades

**HTTP Request**

> GET /api/v1/public?command=returnTradeHistory

`curl "https://api.coinw.fm/api/v1/public?command=returnTradeHistory&symbol=CWT_CNYT&start=1579238517000&end=1581916917660"`

Request Parameters

Field |	Data Type |	must  |	Description
-------------- | -------------- | --------------| --------------
symbol	| string |  true	  | Trading pair like: BTC_CNYT
start  |	string  |	false	|	Start time：UNIX timestamp
end	|string  |	false	|	End time：UNIX timestamp
Response Content

Field  | Data  Type  |	Description
-------------- | -------------- | --------------
id | string |	Trading ID
type	|string  |	Type
price  |	string  |	Unit
amount|	string  | Total quantity
total	|string  |	Total amount
time	|string  |	Trading time

```json

                  {
                      "code":"200",
                      "data":[
                    {


                         "amount":49.2,
                          "total":160.5888,

                          "price":3.264,
                          "id":416253782,
                          "time":"2020-01-09 10:10:15",
                          "type":"buy"
                      },{
                          "amount":63.4,
                          "total":207.1278,
                          "price":3.267,
                          "id":416253778,
                          "time":"2020-01-09 10:10:15",
                          "type":"sell"
                          }
                      ],
                      "msg":"SUCCESS"
                  }
```
      
  
## <span>K-line data</span>
              

Back to K-line data

**HTTP Request**

>GET /api/v1/public?command=returnChartData

`curl "https://api.coinw.fm/api/v1/public?currencyPair=CWT_CNYT&command=returnChartData&period=1800&start=1580992380&end=1582288440"`

Request Parameters

Field  |  Data Type	|  must		|  Description
-------------- | -------------- | --------------| --------------
period	| Int	|True	  |  Cycle: Sec. such as: 60, 180, 300, 900, 1800, 7200, 14400
currencyPair 	| String	| True	|	| Trading pair like: BTC_CNYT
start	|String	|  False	|	Start | time:UNIX timestamp
end	|String	|  False	|	End | time:UNIX timestamp
Response Content

Field	| Data Type	| Description
-------------- | -------------- | --------------
date|	string	| Time
high|	string	| High
low	|string  |	Low
open	|  string 	|  Open
close	|  string    | 	Close
volume	|string	| Volume

```json
        {
          "code":"200",
          "data":[{
              "date":1.5809922E12,
              "volume":0.0,
              "high":8.803,
              "low":8.803,
              "close":8.803,
              "open":8.803
            },{
              "date":1.580994E12,
              "volume":0.0,
              "high":8.803,
              "low":8.803,
              "close":8.803,
              "open":8.803
            },{
              "date":1.5822864E12,
              "volume":121503.276,
              "high":9.587,
              "low":9.169,
              "close":9.4949,
              "open":9.4274
            },{
              "date":1.5822882E12,
              "volume":137447.694,
              "high":9.575,
              "low":9.191,
              "close":9.4599,
              "open":9.4949
            }
          ],
          "msg":"SUCCESS"
        }
```      
## <span>Hot currency volume</span>

Get trading pair 24H volume

**HTTP Request**

>GET /api/v1/public?command=return24hVolume

`curl "https://api.coinw.fm/api/v1/public?command=return24hVolume"`

Request Parameters

No parameter is needed for this endpoint.

Response Content


```json
        {
          "code":"200",
          "data":{
            "totalETH":"0",
            "USDT_CNYT":{
              "USDT":"9507323.2456",
              "CNYT":"66883008.0578"
            },
            "totalUSDT":"375022045.7914",
            "ETH_USDT":{
              "ETH":"0",
              "USDT":"0"
            },
            "totalBTC":"0",
            "CWT_CNYT":{
              "CWT":"6003449.28",
              "CNYT":"55189103.6876"
            },
            "BTC_CNYT":{
              "BTC":"46550.1319",
              "CNYT":"2516207980.3979"
            },
            "BTC_USDT":{
              "BTC":"0",
              "USDT":"0"
            },
            "ETH_CNYT":{
              "ETH":"0",
              "CNYT":"0"
            }
          },
          "msg":"SUCCESS"
        }
```      
# Trade API

For fast trading

## <span>Pending order list</span>

Back to the trading pair's pending order list

**HTTP Request**

>POST /api/v1/private?command=returnOpenOrders

`curl "https://api.coinw.fm/api/v1/private?command=returnOpenOrders"`

Request Parameters

Field	 |Data Type |	must	 |	Description
-------------- | -------------- | --------------| --------------
currencyPair	 |string	 |true	 |	Trading pair

Response Content

Field |	Data Type	 |Description
-------------- | -------------- | --------------
orderNumber |	string |	Order no.
date	 |string |	Trading time
startingAmount |	string |	Order total amount
total	 |string |	Total order
type	 |string	 |Order type
prize	 |string	 |Order price
success_count	 |string	 |Total traded quantity
success_amount |	string	 |Total traded amount
status |	string |	Status: 1-pending, 2-partial pending, 3-all completed, 4-user cancel

```json
                {
                    "code":"200",
                    "data":[
                        {
                        "orderNumber":421547953,
                        "date":1577419268000,
                        "startingAmount":11,
                        "total":11,
                        "type":"buy",
                        "prize":1,
                        "success_count":0,
                        "success_amount":0,
                        "status":1
                        }
                    ],
                    "msg":"SUCCESS"
                }
```      

## <span>Order details</span>
      
Back to the order detail information

**HTTP Request**

>POST /api/v1/private?command=returnOrderTrades

`curl "https://api.coinw.fm/api/v1/private?command=returnOrderTrades"`

Request Parameters

Field	| Data Type  |	must   |	Description
-------------- | -------------- | --------------| --------------
orderNumber	| string	|  true	|	Order

Response Content

Field	| Data Type	|  Description
-------------- | -------------- | --------------
tradeID	| string	|  Trading ID |
currencyPair	| string	|  Trading pair |
type	 |string	|  Order type
amount |	string |	Total trading amount
success_amount |	string |	Traded amount
total	 |string	 |Total order
success_total	 |string |	Traded quantity
fee	 |string |	Unit
date	 |string	 |Trading time
status |	string	 |Status: 1-pending, 2-partial pending, 3-all completed, 4-user cancel

```json
                  {
                      "code":"200",
                      "data":{
                          "tradeID":421547953,
                          "currencyPair":"CWT_CNYT",
                          "type":"buy",
                          "amount":11,
                          "success_amount":0,
                          "total":11,
                          "success_total":"0.00",
                          "fee":1,
                          "date":"2019-12-27 12:01:08",
                          "status":1
                      },
                      "msg":"SUCCESS"
                  }
```  


## <span>Order status</span>            


Back to the order satus information

**HTTP Request**

>POST /api/v1/private?command=returnOrderStatus

`curl "https://api.coinw.fm/api/v1/private?command=returnOrderStatus"`

Request Parameters

Field |	Data Type |	must	 |	Description
-------------- | -------------- | --------------| --------------
orderNumber	 |string |	true	 |	Order no.
Response Content

Field	|Data Type|	Description
-------------- | -------------- | --------------
currencyPair|	string|	Trading pair
type|	string|	Order type
total|	string|	Total order
startingAmount	|string|	Order amount
status|	string	|Status: 1-pending, 2-partial pending, 3-all completed, 4-user cancel

```json
                {
                    "code":"200",
                    "data":{
                        "status":1,
                        "currencyPair":"CWT_CNYT",
                        "date":"2019-12-27 12:01:08",
                        "total":11,
                        "type":"buy",
                        "startingAmount":11
                    },
                    "msg":"SUCCESS"
                }
```       
## <span> History order </span>      


Back to the trading pair's traded records, 1000 at most

**HTTP Request**

>POST /api/v1/private?command=returnUTradeHistory

`curl "https://api.coinw.fm/api/v1/private?command=returnUTradeHistory"`

Request Parameters

Field	|Data Type	|must	|	Description
-------------- | -------------- | --------------| --------------
currencyPair|	string	|true	|	Trading pair

Response Content

Field	|Data Type|	Description
-------------- | -------------- | --------------
tradeID	|string|	Trading ID
type|	string	|Order type
amount	|string|	Total trading amount
success_amount|	string|	Traded amount
total	|string	|Total order
success_count	|string	|Traded quantity
fee|	string	|Fee
prize	|string	|Order price
date|	string	|Trading time
status	|string	|Status: 1-pending, 2-partial pending, 3-all completed, 4-user cancel

```json
                {
                    "code":"200",
                    "data":[
                        {
                            "tradeID":421547953,
                            "date":1577419268000,
                            "amount":11,
                            "total":11,
                            "fee":1,
                            "type":"buy",
                            "prize":1,
                            "success_count":0,
                            "success_amount":0,
                            "status":1
                        },{
                            "tradeID":401267521,
                            "date":1573463699000,
                            "amount":111.1011,
                            "total":33.43,
                            "fee":3.323,
                            "type":"buy",
                            "prize":3.323,
                            "success_count":33.43,
                            "success_amount":111.1011,
                            "status":3
                        },{
                            "tradeID":393755271,
                            "date":1573036041000,
                            "amount":138.7007,
                            "total":39.18,
                            "fee":3.54,
                            "type":"buy",
                            "prize":3.54,
                            "success_count":39.18,
                            "success_amount":138.7007,
                            "status":3
                        }
                    ],
                    "msg":"SUCCESS"
                }
```      

## <span> Order </span> 
      

Order

**HTTP Request**

>POST /api/v1/private?command=doTrade

`curl "https://api.coinw.fm/api/v1/private?command=doTrade"`

Request Parameters

Field|	Data Type|	must|	Description
-------------- | -------------- | -------------- | --------------
symbol|	string|	true	|	Trading pair like: BTC_CNYT
type|	string	|true	|	Order type: 0-buy, 1-sell
amount	|double	|true	|	Order quantity
rate|	double|	true	|	Order price
Response Content

Field	|Data Type|	Description
-------------- | -------------- | -------------- 
orderNumber	|string	|Order no.

```json
                  {
                      "code":"200",
                      "data":{
                          "orderNumber":422742231
                      },
                      "msg":"SUCCESS"
                  }
```        

## <span> Cancel order </span> 
     

Cancel the order

**HTTP Request**

>POST /api/v1/private?command=cancelOrder

`curl "https://api.coinw.fm/api/v1/private?command=cancelOrder"`

Request Parameters

Field	|Data Type	|must|	Description
-------------- | -------------- | -------------- | -------------- 
orderNumber	|string	|true	|	Order no.
Response Content

Field	 | Data Type	 | Description
-------------- | -------------- | --------------  
clientOrderId	 | string	 | Order no.

```json
                {
                    "code":"200",
                    "data":{
                        "clientOrderId":422744738
                    },
                    "msg":"SUCCESS"
                }
```    

## <span>Cancel all order </span>
   

Cancel all order

**HTTP Request**

>POST /api/v1/private?command=cancelAllOrder

`curl "https://api.coinw.fm/api/v1/private?command=cancelAllOrder"`

Request Parameters

Field	 |Data Type |	must |		Description
-------------- | -------------- | --------------  | -------------- 
currencyPair |	string	 |False	 |	Trading pair

Response Content

Field	| Data Type	| Description
-------------- | -------------- | --------------   
orderNumbers| 	Array	| Order no. list

```json
                {
                    "code":"200",
                    "data":{
                        "orderNumbers":[421547953]
                    },
                    "msg":"SUCCESS"
                }
```
            
# Withdraw API

For fast crypto withdrawal

## <span>Available balance </span>


Return the available balance of the asset account

**HTTP Request**

>POST /api/v1/private?command=returnBalances

`curl "https://api.coinw.fm/api/v1/private?command=returnBalances"`

Request Parameters

No parameter is needed for this endpoint.

Response Content


```json
            {
                "code":"200",
                "data":{
                    "MATIC":0,
                    "TRIO":0,
                    "CTXC":0,
                    "BCHSV":0,
                    "HT":0,
                    "HX":0,
                    "SDA":0,
                    "CDT":0,
                    "GDP":0,
                    "IHT":0,
                    "STX":0,
                    "TNT":0,
                    "BCD":0,
                    "AE":0,
                    "IOST":0.0014,
                    "0X":0
                },
                "msg":"SUCCESS"
            }
```            

## <span>All balance </span>


Return all balances of the asset account

**HTTP Request**

>POST /api/v1/private?command=returnCompleteBalances

`curl "https://api.coinw.fm/api/v1/private?command=returnCompleteBalances"`

Request Parameters

No parameter is needed for this endpoint.

Response Content

Field	| Data Type	| Description
-------------- | -------------- | --------------   
available| 	string	| Available balance
onOrders| 	string	| Lock balance


```json
                {
                    "code":"200",
                    "data":{
                        "MATIC":{
                                "onOrders":0,
                                "available":0
                            },
                            "TRIO":{
                                "onOrders":0,
                                "available":0
                            },
                            "CTXC":{
                                "onOrders":0,
                                "available":0
                            },
                            "BCHSV":{
                                "onOrders":0,
                                "available":0
                            },
                            "HT":{
                                "onOrders":0,
                                "available":0
                            }
                        },
                    },
                    "msg":"SUCCESS"
                }
```      


## <span> D&w history </span>
      
Get d&w history

**HTTP Request**

>POST /api/v1/private?command=returnDepositsWithdrawals

`curl "https://api.coinw.fm/api/v1/private?command=returnDepositsWithdrawa`

Request Parameters

Field	 | Data Type | 	must	 | Description
-------------- | -------------- | --------------    | -------------- 
symbol | 	string | 	true	 | 	Currency name

Response Content

Field |	Data Type |	Description
-------------- | -------------- | --------------    
amount	 |string |	Quantity
depositNumber |	string	 |The only number(ID)
address	 |string |	D&w addresses
txid	 |string |	Trading hash
currency |	string	 |Currency name
confirmations	 |string	 |Confirmations
status	 |string |	Status 1: withdrawing 3: withdrawn 4: user cancel

```json
              {
                "code":"200",
                "data":[
                    {
                        "amount":31659.654543,
                        "depositNumber":937963,
                        "address":"123",
                        "txid":"已提交autocoinone937963Mon Oct 08 20:19:25 CST 2018",
                        "currency":"HC",
                        "confirmations":0,
                        "status":3
                    },{
                        "amount":398.8,
                        "depositNumber":903010,
                        "address":"123",
                        "txid":"已提交autocoinone903010Fri Aug 31 18:26:16 CST 2018",
                        "currency":"HC",
                        "confirmations":0,
                        "status":3
                    }
                ],
                "msg":"SUCCESS"
              }
``` 

## <span> Withdraw </span>

         
Withdraw

**HTTP Request**

>POST /api/v1/private?command=doWithdraw

`curl "https://api.coinw.fm/api/v1/private?command=doWithdraw"`

Request Parameters

Field|	Data Type	|must|	Description
-------------- | -------------- | --------------  | --------------     
memo|	string|	False	|	Memo
amount	|string	|true	|	Withdraw quantity
currency|	string|	true	|	Currency
address|	string	|true	|	Withdrawal address
Response Content


```json
                {
                    "code": "200",
                    "data": null,
                    "msg": "SUCCESS"
                }
```     



## <span> Cancel withdrawal </span>
         
Cancel withdrawal

**HTTP Request**

>POST /api/v1/private?command=cancelWithdraw

`curl "https://api.coinw.fm/api/v1/private?command=cancelWithdraw"`

Request Parameters

Field|	Data Type|	must	|Description
-------------- | -------------- | --------------  | --------------     
id	|string	|true	|	Withdrawal application id
Response Content


```json
              {
                    "code": "200",
                    "data":null,
                    "msg": "SUCCESS"
                }
```            

# Real-time quotes

Get current market data

## <span> Websocket market data </span>

Websocket market data

**HTTP Request**

websocket /websocket

websocket "wss://api.coinw.fm//websocket"

Request Parameters

Field| 	Data Type	| must	| 	Description
-------------- | -------------- | --------------  | --------------     
event| 	string	| True	| 	Fill inaddChannel
channel	| string	| True	| 	Fill in/market
symbol| 	string	| int	| 	CurrencyID
Response Content

Field |	Data Type |	Description
-------------- | -------------- | --------------       
buy |	Double	 |Buy price
sell |	Double	 |Sell price
high |	Double	 |High 24H
low |	Double	 |Low price
vol |	Double	 |Hot currency volume
last |	Double	 |Latest price

```json
          {
              "channel":"/market",
              "res":{
                  "code":"0",
                  "data":{
                      "buy":50.0,
                      "sell":50.0,
                      "data":{
                          "last":50.0,
                          "high":0.0,
                          "low":0.0,
                          "vol":0.0
                      }
                  },
                  "success":true
              }
          }
```      
# Error code

API interface call error code description

Error code| 	Detail description
-------------- | --------------        
200	| Operation success
500| 	Operation failure
10001	| Internet error
10002	| API not exist
10003	| Parameter error
10004	| No trading permission
10005| 	No withdrawal permission
10006| 	api_key error
10007	| Signature error



