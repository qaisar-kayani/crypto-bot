# Arbitrage opportunity tracker

This Python application listens to centralised cryptocurrency exchange orderbooks to track arbitrage opportunities between exchanges.

When there is an arbitrage opportunity an alert is generated.


# Features

It will show the arbitration opportunities between exchanges. Currently Python logging output support.

```
BTC/GBP #1 (@0.0400 BTC) is 0.09564%  by buy Coinbase   41,875.95  - sell Bitfinex   - 41,916.00  (40.05 GBP)
BTC/GBP #2 (@0.0400 BTC) is 0.03556%  by buy Coinbase   41,875.95  - sell Bitstamp   - 41,890.84  (14.89 GBP)
BTC/EUR #1 (@0.0400 BTC) is 0.05433%  by buy Coinbase   49,428.15  - sell Bitfinex   - 49,455.00  (26.85 EUR)
BTC/EUR #2 (@0.0400 BTC) is 0.05261%  by buy Kraken     49,429.00  - sell Bitfinex   - 49,455.00  (26.00 EUR)
ETH/GBP #1 (@0.5000 ETH) is 0.06897%  by buy Coinbase   2,755.40   - sell Bitfinex   - 2,757.30   (1.90 GBP)
ETH/GBP #2 (@0.5000 ETH) is 0.05082%  by buy Kraken     2,755.90   - sell Bitfinex   - 2,757.30   (1.40 GBP)
ETH/EUR #1 (@0.5000 ETH) is 0.04951%  by buy Coinbase   3,251.69   - sell Bitfinex   - 3,253.30   (1.61 EUR)
ETH/EUR #2 (@0.5000 ETH) is 0.01998%  by buy Bitstamp   3,252.65   - sell Bitfinex   - 3,253.30   (0.65 EUR)
```

The ask and bid levels on specified depth levels can be written to Redis Timeseries database.

A Telegram alert can be send if the arbitration profitabiltiy reaches a certain level. 

# Running

```shell
python ./main.py --no-live
```

# Configuring the Python Telegram bot for a group chat 

Get a Telegram API key from Botfather.

Add the bot in to a chat group.

Query active messages using JQ.


# Get the chat messages for the bot and extract chat id from those
curl https://api.telegram.org/bot$TELEGRAM_API_KEY/getUpdates | jq

export TELEGRAM_CHAT_ID="-111113672"
```
You can query it. For example to get Bitfinex ETH-EUR ask prices all-time.
```
127.0.0.1:6379> TS.RANGE "Orderbook depth: Bitfinex ETH-EUR ask at 3" - + AGGREGTION avg
 1) 1) (integer) 1634236371966
    2) 3252.50454148169
 2) 1) (integer) 1634236373112
    2) 3252.43330625139
...

# Background

This pile of scripts was originally created to see what fiat pair arbitrage opportunities there exists in the markets. The code is designed for crude arbitrage, not for high-frequency systems. The main goal is to have easily modifieable code base.

