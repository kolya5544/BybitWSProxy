# Bybit WSS Demo Proxy (BybitWSProxy)
## WebSocket Trade proxy for your Bybit Demo Account

BybitWSProxy is a server-side application that allows you to accept WebSocket Trade connection, and send them as a REST request to Bybit API instead

## But why? What is this for?

Ever created a trading bot that uses WS Trade only to be unable to test it on your Bybit Demo Account? Well, this is a solution.

You can host it yourself OR **use one of instances hosted on our server** to test your WS Trade bot without changing ANY of its logic!

*Keep in mind*, this software will NOT make your trades faster, and all the latency of REST API will be at play. This software exists SOLELY to test whether or not order placement using WS Trade works, on Demo Account. DON'T USE THIS FOR HFT (or similar applications), IT'LL BE WAY TOO SLOW!

## I need this - but I don't want to install anything. How do I do it?

Easy! If you don't want to install anything, you can access our public WebSocket Trade endpoint. **Keep in mind, this endpoint is ran by ME, a volunteer, it is NOT guaranteed to work 24/7. USE AT YOUR OWN RISK AND DISCRETION!!!**.

This endpoint is also ratelimited to a global 2 req/s limit, with a max queue size of 100 requests.

For Pybit, use:
```python
ws = WebSocketTrading(
    api_key="xxxxx",
    api_secret="xxxxx",
    domain="nk",
    tld="ax",
    demo=True,
    testnet=False
    )
```

And you're good to go!!

## Tech

We use

- [EmbedIO](https://github.com/unosquare/embedio) - a lightweight HTTP/WebSocket library
- [Bybit.Net](https://github.com/JKorf/Bybit.Net) - API connector for C# by JKorf

## Installation

BybitWSProxy requires at least .NET 8

Build the project:
```sh
dotnet build
```

Start BybitWSProxy:
```sh
cd bin/Debug/net8.0
dotnet BybitWSProxy.dll
```

You're good to go! You can now go to `Usage`

## Usage

You will need nginx or Apache to ensure HTTPS/WSS connection to your local WS (insecure) endpoint. Pybit and most other libraries expect WSS, so that is a NECESSITY.

**YOU WILL NEED TO GET A CERTIFICATE FOR `stream-demo` ENDPOINT. Keep that in mind.**

You'll find your WS endpoint, by default, at `ws://localhost:8054/v5/trade`, so once you get a certificate for your local domain (let's say `stream-demo.mylocaldomain.me`), you should be able to connect using pybit:
```python
ws = WebSocketTrading(
    api_key="xxxxx",
    api_secret="xxxxx",
    domain="mylocaldomain",
    tld="me",
    demo=True,
    testnet=False
    )
```

## Development

Only bugfixes and adjustments, please

## Docker

TBD

## License

MIT
