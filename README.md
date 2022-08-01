# Exchange-official-API-docs

#### Official Documentation for the Exchange APIs and Streams
- [Introduction](#Introduction)
- [Getting Started](#startToUse)
- [Encrypted Verification of API](#a1)
	- [Request Process](#a2)

- [API Reference](#b3)
	- [open-api](#b4)
 		-   [summary of every single contract](#1)
 		-   [the specification of the contracts](#2)
 		-   [order book information](#3)

# <span id="Introduction">Introduction</span>

Welcome to [Exchange](https://oval.exchange) API document for developers.

This file provides the related API application introduction. 

---

# <span id="startToUse">Getting Started</span>
REST, a.k.a Respresntational State Transfer, is an architectural style that defines a set of constraints and properties based on HTTP. REST is known for its clear structure, readability, standardization and scalability. Its advantages are as follows:

- Each URL represents one web resource in RESTful architecture.
- Acting as a representation of resources between client and server.
- Client is enabled to operate server-side resources with 4 HTTP requests - representational state transfer.

Developers are recommended to use REST API to proceed spot trading and withdrawals.

# <span id="a1">Encrypted Verification of API</span>


## <span id="a2">Request Process</span>

The root URL for REST access：``` https://oval.exchange ```

###  <span id="a7">Request</span>
All requests are based on Https protocol, contentType in the request header must be uniformly set as: ‘application/x-www-form-urlencoded’.

**Request Process Descriptions**

1、Request parameter: parameter encapsulation based on the port request.

2、Submitting request parameter: submit the encapsulated parameter request to the server via POST/GET/PUT/DELETE or other methods.

3、Server response: the server will first perform a security validation, then send back the requested data to the client in JSON format.

4、Data processing: processing server response data.

**Success**

HTTP status code 200 indicates a successful response and may contain content. If the response contains content, it will appear in the corresponding returned content.

**Common Error Code**

- 400 Bad Request – Invalid request format

- 401 Unauthorized – Invalid API Key

- 403 Forbidden – You do not have access to the requested resource

- 404 Not Found

- 429 Too Many Requests

- 500 Internal Server Error


# <span id="b3"> API Reference</span>

##  <span id="b4">open-api</span>

### <span id="1">summary of every single contract</span>
1. Interface address: /pub/dex/cmcapi/v1/hq/contracts 
2. Interface Description: provides a summary of every single contract traded on the exchange. 

Return value:

|field|	Example|	explain|
|-----|------|---------|
|errno|	0|	 |
|errmsg|	""|	errcode>0fail|
| data|	as follows:|
```
[
    {
      "ticker_id": "BTC-PERPUSD",
      "base_currency": "BTC",
      "quote_currency": "USDT",
      "last_price": 23297.62,
      "base_volume": 26510436,
      "quote_volume": 624456085106.26,
      "bid": 23283.32,
      "ask": 23297.68,
      "high": 24177.2,
      "low": 23106.53,
      "product_type": "Futures",
      "open_interest": 0,
      "index_price": 0,
      "creation_timestamp": 1609988400000,
      "expiry_timestamp": 1893427200000,
      "funding_rate": 0,
      "next_funding_rate_timestamp": 0
    },
    {
      "ticker_id": "ETH-PERPUSD",
      "base_currency": "ETH",
      "quote_currency": "USDT",
      "last_price": 1682.78,
      "base_volume": 79602147,
      "quote_volume": 135216439312.62,
      "bid": 1681.98,
      "ask": 1683.04,
      "high": 1753.57,
      "low": 1666.04,
      "product_type": "Futures",
      "open_interest": 0,
      "index_price": 0,
      "creation_timestamp": 1619596800000,
      "expiry_timestamp": 1924790400000,
      "funding_rate": 0,
      "next_funding_rate_timestamp": 0
    },
    {
      "ticker_id": "XRP-PERPUSD",
      "base_currency": "XRP",
      "quote_currency": "USDT",
      "last_price": 0.3782,
      "base_volume": 25109361,
      "quote_volume": 9685240.2664,
      "bid": 0.378,
      "ask": 0.3784,
      "high": 0.39867,
      "low": 0.37704,
      "product_type": "Futures",
      "open_interest": 0,
      "index_price": 0,
      "creation_timestamp": 1622023200000,
      "expiry_timestamp": 1937232001000,
      "funding_rate": 0,
      "next_funding_rate_timestamp": 0
    }
  ]
```

|data item |	Explain|
|------------|-----------------------------|
|ticker_id|	Identifier of a ticker with delimiter to separate base/quote, eg. BTC-PERPUSD, BTC-PERPETH, BTC-PERPEUR|
|base_currency|	Symbol/currency code of base pair, eg. BTC|
|quote_currency|	Symbol/currency code of quote pair, eg. ETH|
|last_price|	Last transacted price of base currency based on given quote currency|
|base_volume|	24 hour trading volume in BASE currency|
|quote_volume|24 hour trading volume in QUOTE currency|
|bid|	Current highest bid price|
|ask|	Current lowest ask price|
|high|	Rolling 24-hour highest transaction price|
|low|	Rolling 24-hour lowest transaction price|
|open_interest|	The number of outstanding derivatives  contracts that have not been settled|
|index_price|	Last calculated index price for underlying of contract|
|creation_timestamp|	Start date of derivative|
|expiry_timestamp|	End date of derivative|
|funding_rate|	Current funding rate|
|next_funding_rate_timestamp|	Timestamp of the next funding rate change|


### <span id="2">the specification of the contracts</span>
1. Interface address: /pub/dex/cmcapi/v1/hq/contractSpecifications 
2. Interface Description: Describes the specification of the contracts, mainly the pricing of the contract and its type (vanilla, inverse, or quanto)

Return value:

|field|	Example|	explain|
|-----|------|---------|
|errno|	0|	 |
|errmsg|	""|	errcode>0fail|
| data|	as follows:|
```
{
    "contract_type": "Vanilla",
    "contract_price": 1,
    "contract_price_currency": "USDT"
  }
```

|data item |	Explain|
|------------|-----------------------------|
|contract_type|	Describes the type of contract - Vanilla, Inverse or Quanto?|
|contract_price|	Describes the price per contract.|
|contract_price_currency|	Describes the currency which the contract is priced in (e.g. USD, EUR, BTC, USDT)|

### <span id="3">order book information</span>
1. Interface address: /pub/dex/cmcapi/v1/hq/orderbook/BTCUSDT_SWAP
2. Interface Description: Provide order book information with at least depth = 100 (50 each side) returned for a given market pair/ticker.

Return value:

|field|	Example|	explain|
|-----|------|---------|
|errno|	0|	 |
|errmsg|	""|	errcode>0fail|
| data|	as follows:|
```

    "asks": [
      [
        "23319.72",
        "930"
      ],
      [
        "23322.28",
        "1204"
      ],
      [
        "23335.80",
        "12288"
      ],
      [
        "23343.27",
        "10898"
      ]
    ],
    "bids": [
      [
        "23305.28",
        "110"
      ],
      [
        "23302.72",
        "1204"
      ],
      [
        "23286.65",
        "13482"
      ],
      [
        "23281.76",
        "9710"
      ]
    ],
    "ticker_id": "BTC-PERPUSD",
    "timestamp": "1659345067000"
  }
```

|data item |	Explain|
|------------|-----------------------------|
|ticker_id|	A pair such as "BTC-PERPUSD", with delimiter between different cryptoassets|
|timestamp|Unix timestamp in milliseconds for when the last updated time occurred.|
|bids|	An array containing 2 elements. The offer price and quantity fyor each bid order|
|asks|	An array containing 2 elements. The ask price and quantity for each ask order|
