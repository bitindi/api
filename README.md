 

Bitindi API Documentation

Bitindi REST API version 1.2 provides programmatic access to Optima’s next-generation trading engine.

We strongly recommend that our new customers use API version 1.2 to get the best trading experience. We also recommend that our current traders switch to the newest version 1.2.


DEVELOPMENT GUIDE

API URLs



REST https://bitindi.com/api/v1



Date Time Format

All timestamps are returned in ISO 8601 format or UNIX timestamp in milliseconds (UTC).

Example: "2021-06-03T10:20:49.315Z" or "1614815872000".



Number Format

All currency data, e.g., price, amount, fee, etc., should be precision numbers and have a string representation. Example: "20.4383003".


RATE LIMITING

The following Rate Limits are applied:

for the Market data, the limit is 20 requests per second for one IP; for Trading, the limit is 50 requests per second for one user;
for other requests, the limit is 10 requests per second for one user.

Significantly exceeding the Rate Limits can lead to suspension.




BEST PRACTICES

The Bitindi API development team does its best to bring the best trading experience to API
 
users. This manual contains a set of best practices for using the API as efficiently as possible.



HTTP Persistent Connection

The underlying TCP connection is kept active for multiple requests/responses. Subsequent requests will result in reduced latency as the TCP handshaking process is no longer required.

If you use the HTTP 1.0 client, please ensure it supports the Keep-Alive directive and submit the "Connection: Keep-Alive" header with your request.

Keep-Alive is a part of the HTTP/1.1 or HTTP/2 protocol and is enabled by default on compliant clients. However, you will have to ensure your implementation does not set other values as the connection header.





REST API Reference


HTTP Status Codes

200 OK. Successful request

422 Bad Request. Returns JSON with the error message

401 Unauthorized. Authorization is required or has been failed

403 Forbidden. Action is forbidden

404 Not Found. Data requested cannot be found

429 Too Many Requests. Your connection has been rate limited

500 Internal Server. Internal Server Error

503 Service Unavailable. Service is down for maintenance

504 Gateway Timeout. Request timeout expired






Market Data


Currencies

Get Currencies

/api/v1/currencies
 
Response:

{

"name": "Tether",

"symbol": "USDT",

"decimals": 8,

"type": "coin",

"status": true,

"min_deposit_confirmation": 5,

"deposit_status": true,

"withdraw_status": true,

"deposit_fee": "1.00",

"withdraw_fee": "1.00",

"min_deposit": "10.00000000",

"max_deposit": "0.00000000",

"min_withdraw": "10.00000000",

"max_withdraw": "555.00000000",

},

{

"name": "Ethereum",

"symbol": "ETH",

"decimals": 8,

"type": "coin",

"status": true,

"min_deposit_confirmation": 10,

"deposit_status": true,

"withdraw_status": true,

"deposit_fee": "1.50",

"withdraw_fee": "1.50",

"min_deposit": "0.10000000",

"max_deposit": "0.00000000",

"min_withdraw": "0.10000000",

"max_withdraw": "50.00000000",

},

}




Get Market Ticker

/api/v1/markets/ticker

Response:
 

{

"name": "BTC-USDT",

"base_currency": "BTC",

"base_currency_name": "Bitcoin",

"base_currency_type": "coin",

"quote_currency": "USDT",

"quote_currency_name": "Tether",

"quote_currency_type": "coin",

"base_precision": 4,

"quote_precision": 2,

"min_trade_size": "0.00010000",

"max_trade_size": "1000.00000000",

"min_trade_value": "0.00010000",

"max_trade_value": "100000.00000000",

"base_ticker_size": "0.00010000",

"quote_ticker_size": "0.01000000",

"trade_status": true,

"buy_order_status": true,

"sell_order_status": true,

"cancel_order_status": true,

"last": "55180.83",

"change": "-0.24",

"high": "55180.83",

"low": "53989.98",

"volume": "358.0000",

"capitalization": "5.40"

},

{

"name": "ETH-USDT",

"base_currency": "ETH",

"base_currency_name": "Ethereum",

"base_currency_type": "coin",

"quote_currency": "USDT",

"quote_currency_name": "Tether",

"quote_currency_type": "coin",

"base_precision": 4,

"quote_precision": 2,

"min_trade_size": "0.01000000",

"max_trade_size": "1000.00000000",

"min_trade_value": "0.00010000",

"max_trade_value": "10000.00000000",

"base_ticker_size": "0.00010000",

"quote_ticker_size": "0.01000000",
 
"trade_status": true,

"buy_order_status": true,

"sell_order_status": true,

"cancel_order_status": true,

"last": "3609.45",

"change": "0.96",

"high": "3609.45",

"low": "3609.45",

"volume": "91.0000",

"capitalization": "25.13"

},




Get Market Orderbook:

/api/v1/markets/orderbook

Params:

market: Market Name (e.g. BTC-USDT)



Response:

{

"bids": [

{

"price": "54917.40000000",

"quantity": "0.01731000"

},

{

"price": "54916.00000000",

"quantity": "0.04708000"

},

{

"price": "54915.99000000",

"quantity": "0.29948000"

}

],

"asks": [

{

"price": "47832.80000000",

"quantity": "0.04320000"
 
},

{

"price": "47835.34000000",

"quantity": "0.05480000"

},

{

"price": "47856.25000000",

"quantity": "1.72250000"

}

]

}




Get Market Trades:

/api/v1/markets/trades

Params:

market: Market Name (e.g. BTC-USDT)



Response:

"data": [

{

"side": "buy",

"price": "53998.04000000",

"quantity": "84.00000000",

"created_at": "2021-10-07 22:41:29"

},

{

"side": "buy",

"price": "54134.97000000",

"quantity": "98.00000000",

"created_at": "2021-10-07 22:13:27"

}

]

