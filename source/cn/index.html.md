---
title: Exchange官方API文档

language_tabs: # must be one of https://git.io/vQNgJ
  

toc_footers:

includes:
  
language: 简体中文

other_language: English

url: /docs/en

present_url: /docs/cn

active: active

other_active:

menu: 菜单


spot_goods: 现货

spot_goods_active: active

searchText: 搜索

search: true

code_clipboard: true
---

# API简介
**欢迎使用CoinW API**

此文档是CoinWAPI的唯一官方文档，CoinWAPI提供的能力会在此持续更新，请大家及时关注。

你可以通过点击上方菜单来切换获取不同业务的API，还可通过点击右上方的语言按钮来切换文档语言。

## <span>描述</span>

1、获取API认证的api key和secret key

申请API即可获得api key和secret key，其中api key是提供给API用户的访问密钥，secret key用于对**请求参数**签名的私钥。 注意： 请勿向任何人泄露这两个参数，这两个参数关乎账号安全。

2、生成待签名字符串

用户提交的参数除sign外，都要参与签名。 待签名字符串要求按照参数名进行排序（首先比较所有参数名的第一个字母，按abcd顺序排列，若遇到相同首字母,则看第二个字母, 以此类推。） 例如：对于如下的参数进行签名 `string[] parameters={"api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c"，"symbol=btc_cny"type=0"price=680"amount=1.0"}; 生成待签名字符串为：amount=1.0&api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c&price=680&symbol=btc_cny&type=0`

3、MD5签名

在MD5签名时,需要私钥secret key参与签名。 将待签名字符串添加私钥参数生成最终待签名字符串， 例如：amount=1.0&api_key=c821db84-6fbd-11e4-a9e3-c86000d26d7c&price=680&symbol=btc_cny&type=0&secret_key=secretKey 注意“&secret_key=secretKey” 为签名必传参数。 利用32位MD5算法 对最终待签名字符串进行签名运算,从而得到签名结果字符串(该字符串赋值于参数 sign)，MD5计算结果中字母全部大写。


## <span>联系我们</span>

使用过程中如有问题或者建议，您可选择以下任一方式联系我们：

加入官方QQ群（967798979），进群时请注明UID 和编程语言。



# 基础API

## <span>获取交易对摘要信息</span>

获取币赢的交易市场基础信息。 其他api接口使用的symbol参数从此处获取，所以使用其他api前，请先通过此api获取必要的信息。

检索交易所中列出的每个货币对的摘要信息

**HTTP 请求**

> GET /api/v1/public?command=returnTicker

`curl "https://api.coinw.uk/api/v1/public?command=returnTicker"`

**请求参数**

此接口不接受任何参数。


|参数名称	|数据类型|	描述|
-------------- | -------------- | --------------
|id	|string	|id|
|last	|string	|最新成交价|
|lowestAsk	|string	|最低卖价|
highestBid	|string	|最高买价|
percentChange	|string	|涨跌幅|
isFrozen	|string	|是否冻结|
high24hr	|string	|24小时最高价|
low24hr	|string	|最低价|
baseVolume	|string	|基础币种24小时交易量|

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
## <span>币种信息</span>

返回币种的相关信息

**HTTP 请求**

> GET/api/v1/public?command=returnCurrencies

`curl "https://api.coinw.uk/api/v1/public?command=returnCurrencies"`

**请求参数**

此接口不接受任何参数。

**返回字段**

参数名称|	数据类型|	描述|
-------------- | -------------- | --------------
maxQty	|string	|最大提币量|
minQty|	string	|最小提币量
recharge	|string	|是否能够充值，0不能1可以
symbol|	string	|币种
symbolId|	string	|币种符号
txFee	|string	|手续费
withDraw	|string	|是否能够提现，0不能1可以
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

## <span>交易对信息</span>

返回交易对的相关信息

**HTTP 请求**

> GET/api/v1/public?command=returnSymbol

`curl "https://api.coinw.uk/api/v1/public?command=returnSymbol"`

**请求参数**

此接口不接受任何参数。

**返回字段**

| 字段 |含义|例子
-------------- | -------------- | -------------- 
|currencyPair| 交易对|"lat_USDT"|
|currencyBase| 交易对中的基础币种|"lat"|
|currencyQuote| 交易对中的计价币种|"USDT|
|maxBuyCount| 最大挂单数量|"99999999"|
|minBuyCount| 最小挂单数量|"0.001"|
|pricePrecision|价格精度 |4|
|countPrecision|数量精度| 4|
|minBuyAmount|最小挂单金额| "10.0"|
|maxBuyAmount| 最大挂单金额|"99999999"|
|minBuyPrice| 最小挂单价格|"99999999"|
|maxBuyPrice| 最大挂单价格|"99999999"|
|state|1：正常 2：禁用 |1|


```json

 { "code": "200",
  "data": [
    {
      "currencyBase": "BTC3L",
      "maxBuyCount": "99999999",
      "pricePrecision": 6,
      "minBuyPrice": "0.0000010",
      "currencyPair": "BTC3L_USDT",
      "minBuyAmount": "5.0",
      "maxBuyPrice": "99999999",
      "currencyQuote": "USDT",
      "countPrecision": 3,
      "minBuyCount": "0.001",
      "state": 1,
      "maxBuyAmount": "99999999"
    }
]
}
```
# 行情API

获取最新市场行情数据

 ## <span>获取深度</span>


返回给定交易对的深度信息

**HTTP 请求**

> GET /api/v1/public?command=returnOrderBook

`curl "https://api.coinw.uk/api/v1/public?command=returnOrderBook&symbol=BTC_CNYT&size=20"`

**请求参数**

参数名称| 	数据类型| 	必须| 	默认值	| 描述
-------------- | -------------- | -------------- | -------------- | -------------- 
size	| Int	| false|  	5	| 深度大小 （5，20）
symbol	| string| 	true	| 	| 交易对如：BTC_CNYT

**返回字段**

参数名称|	数据类型	|描述
-------------- | -------------- | --------------
asks	|string	|买方深度
bids	|string	|卖方深度
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

 ## <span>交易对最近成交</span>

返回给定交易对的过去200笔交易

**HTTP 请求**

> GET /api/v1/public?command=returnTradeHistory

`curl "https://api.coinw.uk/api/v1/public?command=returnTradeHistory&symbol=CWT_CNYT&start=1579238517000&end=1581916917660"`

**请求参数**

参数名称|	数据类型	|必须|	描述
-------------- | -------------- | -------------- | -------------- | 
symbol	|string|	true	|	交易对如：BTC_CNYT
start	|string	|false	|	开始时间：UNIX时间戳
end|	string	|false		|结束时间：UNIX时间戳

**返回字段**

参数名称|	数据类型	|描述
-------------- | -------------- | -------------- | 
id	|string	|交易ID
type|	string	|买卖类型
price|	string	|单价
amount|	string	|总数量
total|	string	|总金额
time|	string|	交易时间
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
## <span>K线数据</span>


返回k线数据

**HTTP 请求**

> GET /api/v1/public?command=returnChartData

`curl "https://api.coinw.uk/api/v1/public?currencyPair=CWT_CNYT&command=returnChartData&period=1800&start=1580992380&end=1582288440"`

**请求参数**

参数名称|	数据类型|	必须		|描述
-------------- | -------------- | -------------- | -------------- | 
period|	Int|	True	|	周期：单位秒，如：60，180，300, 900, 1800, 7200, 14400
currencyPair|	String|	True	|	交易对如：BTC_CNYT
start|	String|	False	|	开始时间:UNIX时间戳
end|	String	|False	|	结束时间:UNIX时间戳

**返回字段**

参数名称| 	数据类型	| 描述
-------------- | -------------- | -------------- 
date	| string	| 时间
high| 	string	| 高
low	| string	| 低
open| 	string	| 开
close	| string| 	收
volume	| string	| 成交量
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

## <span>热门币种成交量</span>

获取热门市场24小时成交量

**HTTP 请求**

> GET /api/v1/public?command=return24hVolume

`curl "https://api.coinw.uk/api/v1/public?command=return24hVolume"`

**请求参数**

此接口不接受任何参数。

**返回字段**

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

## 交易API

用于快速进行交易

## <span>未完成订单列表</span>


返回指定交易对的未完成订单列表

**HTTP 请求**

> POST /api/v1/private?command=returnOpenOrders

`curl "https://api.coinw.uk/api/v1/private?command=returnOpenOrders"`

**请求参数**

参数名称|	数据类型	|必须	|	描述
-------------- | -------------- | --------------  | --------------  
currencyPair	|string	|true	|	交易对
startAt	|long	|false	|	起始时间
endAt	|long	|false	|	结束时间


**返回字段**

参数名称 |	数据类型	 |描述
-------------- | -------------- | --------------    
orderNumber |	string	 |订单号
date	 |string |	交易时间
startingAmount |	string	 |订单总金额
total |	string 	 |订单总量
type |	string	 |订单类型
prize	 |string	 |委托价格
success_count	 |string	 |成交的总数量
success_amount |	string	 |成交的总金额
status	 |string	 |状态:1-未完成、2-部分成交、3-完全成交、4-用户撤销
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
  
## <span>订单详情</span>
            
返回指定订单的详细信息

**HTTP 请求**

> POST /api/v1/private?command=returnOrderTrades

`curl "https://api.coinw.uk/api/v1/private?command=returnOrderTrades"`

**请求参数**

参数名称| 	数据类型	| 必须	| 	描述
-------------- | -------------- | -------------- |--------------
orderNumber| 	string	| true	| 	| 订单号

**返回字段**

参数名称|	数据类型	|描述
-------------- | -------------- | --------------
tradeID	|string|	交易ID
currencyPair|	string	|交易对
type|	string|	订单类型
amount	|string	|交易总金额
success_amount|	string	|已成交金额
total|	string|	订单总量
success_total|	string|	已成交数量
fee	|string|	单价
date	|string	|交易时间
status	|string|	状态:1-未完成、2-部分成交、3-完全成交、4-用户撤销
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

## <span>订单状态</span>  


返回指定订单的状态信息

**HTTP 请求**

> POST /api/v1/private?command=returnOrderStatus

`curl "https://api.coinw.uk/api/v1/private?command=returnOrderStatus"`

**请求参数**

参数名称	|数据类型|必须	|	描述
-------------- | -------------- | --------------| --------------
orderNumber|	string	|true|订单号
**返回字段**

参数名称|	数据类型	|描述
-------------- | -------------- | --------------
currencyPair|	string	|交易对
type|	string	|订单类型
total	|string	|订单总量
startingAmount	|string	|订单金额
status	|string	|状态:1-未完成、2-部分成交、3-完全成交、4-用户撤销

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
  
## <span>历史订单</span>  

返回指定交易对的历史订单，最多1000条

**HTTP 请求**

> POST /api/v1/private?command=returnUTradeHistory

`curl "https://api.coinw.uk/api/v1/private?command=returnUTradeHistory"`

**请求参数**

参数名称	|数据类型	|必须	|	描述
-------------- | -------------- | -------------- | --------------
currencyPair|	string|	true|		交易对
startAt	|long	|false	|	起始时间
endAt	|long	|false	|	结束时间

**返回字段**

参数名称	 | 数据类型	 | 描述
-------------- | -------------- | -------------- 
tradeID	 | string | 	交易ID
type	 | string | 订单类型
amount	 | string	 | 交易总金额
success_amount	 | string	 | 已成交金额
total | 	string	 | 订单总量
success_count | 	string	 | 已成交数量
fee	 | string	 | 手续费
prize	 | string	 | 委托价格
date	 | string	 | 交易时间
status	 | string	 | 状态:1-未完成、2-部分成交、3-完全成交、4-用户撤销

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
## <span>历史成交</span>  

返回指定交易对的历史成交，每次最多100条

**HTTP 请求**

> POST /api/v1/private?command=getUserTrades

`curl "https://api.coinw.uk/api/v1/private?command=getUserTrades"`

**请求参数**

参数名称	|数据类型	|必须	|	描述
-------------- | -------------- | -------------- | --------------
|symbol| string | N | 币种对名称：LTC_USDT
|startAt| long | N | 开始时间：时间戳
|endAt | long | N | 结束时间：时间戳
|limit|int|N|查询条数  0<limit<=100（不传默认20）
|before|long|N|翻页用（上一次调用此接口返回的值，如有）
|after|long|N|翻页用（上一次调用此接口返回的值，如有）
      
**返回字段**

参数名称	 | 数据类型	 | 描述
-------------- | -------------- | --------------   
|tradeId| long | 成交ID
|orderId| long | 订单ID
|price| string | 成交价格
|size | string | 成交数量
|side | string | 成交方向 buy , sell
|orderType| string | 成交类型 limit
|time| long | 成交时间
| fee| double | 手续费
|before|long|翻页用（如有）
|after|long|翻页用（如有）    
      
```json
{
    "code": "200",
    "data": {
        "before": 1125899907141206079,
        "after": 1125899907141206202,
        "list": [
            {
                "fee": 0.14,
                "orderId": 4612803122241208330,
                "orderType": "LIMIT",
                "price": 7E+1,
                "side": "BUY",
                "size": 1,
                "time": 1628068267298,
                "tradeId": 1029953
            }
]
}
}
```      
      
## <span>下单</span>     


下订单

**HTTP 请求**

> POST /api/v1/private?command=doTrade

`curl "https://api.coinw.uk/api/v1/private?command=doTrade"`

**请求参数**

参数名称|	数据类型|	必须		|描述
-------------- | -------------- | -------------- | --------------
symbol	|string	|true|		交易对如：BTC_CNYT
type	|string	|true	|	委托类型：0-买单、1-卖单
amount	|double	|true	|	委托数量
rate	|double	|true|		委托价格
**返回字段**

参数名称|	数据类型	|描述
-------------- | -------------- | -------------- 
orderNumber	|string	|订单号

```json

                  {
                      "code":"200",
                      "data":{
                          "orderNumber":422742231
                      },
                      "msg":"SUCCESS"
                  }
   ```     

## <span>撤销订单</span>       


撤销指定订单

**HTTP 请求**

> POST /api/v1/private?command=cancelOrder

`curl "https://api.coinw.uk/api/v1/private?command=cancelOrder"`

**请求参数**

参数名称|	数据类型	|必须	|	描述
-------------- | -------------- | --------------  | --------------
orderNumber|	string	|true		|订单号

**返回字段**

参数名称| 	数据类型	| 描述
-------------- | -------------- | -------------- 
clientOrderId	| string| 	订单号

```json

                {
                    "code":"200",
                    "data":{
                        "clientOrderId":422744738
                    },
                    "msg":"SUCCESS"
                }
   
```
      

## <span>撤销所有订单</span>        
         
撤销所有订单

**HTTP 请求**

> POST /api/v1/private?command=cancelAllOrder

`curl "https://api.coinw.uk/api/v1/private?command=cancelAllOrder"`

**请求参数**

参数名称 | 	数据类型 | 	必须	 | 	描述
-------------- | -------------- | -------------- | -------------- 
currencyPair | 	string	 | False	 | 	交易对
**返回字段**

参数名称 | 	数据类型	 | 描述
-------------- | -------------- | --------------  
orderNumbers	|Array	|订单号列表
```json

                {
                    "code":"200",
                    "data":{
                        "orderNumbers":[421547953]
                    },
                    "msg":"SUCCESS"
                }

   
```         


# 提现API

用于快速进行虚拟币提现

## <span>可用余额</span>        

返回币币账户的可用余额

**HTTP 请求**

> POST /api/v1/private?command=returnBalances

`curl "https://api.coinw.uk/api/v1/private?command=returnBalances"`

**请求参数**

此接口不接受任何参数。

**返回字段**

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

## <span>所有余额</span>        

返回币币账户的所有余额

**HTTP 请求**

> POST /api/v1/private?command=returnCompleteBalances

`curl "https://api.coinw.uk/api/v1/private?command=returnCompleteBalances"`

**请求参数**

此接口不接受任何参数。

**返回字段**

参数名称 |	数据类型	 |描述
-------------- | -------------- | --------------  
available |string	 |可用余额
onOrders |	string	 |冻结余额

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

## <span>充提记录</span>        
    
获取充提记录

**HTTP 请求**

> POST /api/v1/private?command=returnDepositsWithdrawals

`curl "https://api.coinw.uk/api/v1/private?command=returnDepositsWithdrawa`

**请求参数**

参数名称|	数据类型	|必须 |	描述
-------------- | -------------- | --------------  | --------------
symbol|	string	|true	|	币种名
**返回字段**

参数名称 |	数据类型	 |描述
-------------- | -------------- | --------------  
amount	 |string	 |数量
depositNumber |	string	 |唯一编号（ID）
address	 |string	 |充提地址
txid |	string	 |交易hash
currency |	string	 |币种名
confirmations |	string	 |确认树
status	 |string	 |状态１:等待提现 3.提现成功 4.用户撤销
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
         
         
## <span>提现</span>        

提现

**HTTP 请求**

> POST /api/v1/private?command=doWithdraw

`curl "https://api.coinw.uk/api/v1/private?command=doWithdraw"`

**请求参数**

参数名称	 |数据类型	 |必须		 |描述
-------------- | -------------- | --------------  | --------------  
memo	 |string	 |False	 |	Memo
amount	 |string	 |true	 |	 |提现数量
currency	 |string |	true	 |	币种
address	 |string	 |true	 |	提币地址
**返回字段**

```json

                {
                    "code": "200",
                    "data": null,
                    "msg": "SUCCESS"
                }
    
```      


## <span>取消提现</span>            


取消提现

**HTTP 请求**

> POST /api/v1/private?command=cancelWithdraw

`curl "https://api.coinw.uk/api/v1/private?command=cancelWithdraw"`

**请求参数**

参数名称| 	数据类型| 	必须	| 描述
-------------- | -------------- | --------------  | --------------  
id| 	string	| true		| 提币申请id
**返回字段**

```json

              {
                    "code": "200",
                    "data":null,
                    "msg": "SUCCESS"
                }
   
```
         
# 实时行情

获取最新市场行情数据

## <span>前置准备</span>        

前置准备


**在创建WebSocket连接前， 需使用Http方式调用以下接口，根据返回信息进行连接创建**

`https://www.coinw.uk/pusher/public-token`

**请求参数**
无

**返回字段**

参数名称	 |数据类型 |	描述
-------------- | -------------- | --------------    
token |	string |	发起WebSocket时所需身份信息
endpoint |	string	 |发起WebSocket时连接地址信息
protocol |	string	 |协议
timestamp |	long	  |服务器时间
expiredTime |	long	 |过期时间
pingInterval |	long	 |心跳检查周期,单位毫秒

```json
{
	"success": true,
	"code": 200,
	"message": "success",
	"retry": false,
	"data": {
		"token": "2ae60df9-c4d9-40c6-ad51-465ae7cca06f",
		"endpoint": "wss://ws.coinw.uk",
		"protocol": "websocket",
		"timestamp": 1627379009291,
		"expiredTime": 1627379039291,
		"pingInterval": 10000
	}
}
```

## <span>创建连接</span>

**本WebSocket连接需使用Socket.io框架进行开发，具体开发细则，需根据对应语言获取相应的依赖库。
根据前置信息返回数据中的token和endpoint,组装成连接所需的URL地址,示例如下:**

`wss://ws.coinw.uk/socket.io/?token=87a34709-2c4a-4eab-8bf2-d477d4689dd0&EIO=3&transport=websocket`

## <span>公共行情推送</span>

公共行情推送


**请求参数**

参数名称	 |值 |	描述
-------------- | -------------- | --------------    
event |	subscribe | 订阅
args |	spot/market-api-ticker:${symbol}	 |${symbol}为所需订阅的币种，例如:LTC-USDT


**返回字段**

参数名称	 |数据类型 |	描述
-------------- | -------------- | --------------    
channel |	string |	订阅的通道
subject |	string	 |所属科目
buy |	bigdecimal	 | 买一价
changePrice |	bigdecimal	  |涨跌额
changeRate |	bigdecimal	 |涨跌幅
high |	bigdecimal	 |24小时最高价
last |	bigdecimal	 |最新价
low |	bigdecimal	  |24小时最低价
open |	bigdecimal	 |开盘价
sell |	bigdecimal	 |卖一价
symbol |	string	 |币种
vol |	bigdecimal	  |成交数量
volValue |	bigdecimal	 |成交额

```json

         {
         	"channel": "spot/market-api-ticker:LTC-USDT",
         	"subject": "spot/market-api-ticker",
         	"data": "{\"buy\":\"3.234\",\"changePrice\":\"-0.666\",\"changeRate\":\"-0.170769\",\"high\":\"4.000\",\"last\":\"3.234\",\"low\":\"3.234\",\"open\":\"3.900\",\"sell\":\"4.000\",\"symbol\":\"LTC-USDT\",\"vol\":\"81.360\",\"volValue\":\"306.280240\"}"
         }
   
```   
**data 为字符串， 需根据字符串反序列化成JSON**


```json

        {
        	"buy": "3.234",
        	"changePrice": "-0.666",
        	"changeRate": "-0.170769",
        	"high": "4.000",
        	"last": "3.234",
        	"low": "3.234",
        	"open": "3.900",
        	"sell": "4.000",
        	"symbol": "LTC-USDT",
        	"vol": "81.360",
        	"volValue": "306.280240"
        }
   
``` 
# 错误代码

## <span>API接口调用错误代码描述</span>        

错误代码	|详细描述
-------------- | --------------     
200	|操作成功
500	|操作失败
10001	|网络错误
10002	|API不存在
10003	|参数错误
10004	|无交易权限
10005	|无提现权限
10006	|api_key错误
10007	|签名错误

