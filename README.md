# Binance-Triangular-Arbitrage
This web application screens for triangular arbitrage opportunities on Binance and present it in the UI. You may also toggle the auto trade button to let the underlying code execute trades for you.

Imagine you are a foreign exchange trader in China, and you principal currency is the Chinese Yuan (CNY). You are screening the foreign exchange market and you come accross the following quotes:
USD/CNY: bid: 6.8; ask: 6.9
AUD/USD: bid: 0.76; ask: 0.77
AUD/CNY: bid: 5.5; ask: 5.6

Since you are a smart one and you are good at mental calculation. You quickly realise that if you use 6.9 CNY to purchase 1 USD, you can use that 1 USD to hit the ask order for the AUD/USD currency pair, and buy 1 / 0.77 = 1.29 AUD. You then hit the bid order for the AUD/CNY currency pair to get 7.1 CNY.

You started out with 6.9 CNY and ended up with 7.1 CNY, the trades you just did can be illustrated by the following graph.

            CNY
         //     \\
        AUD ===  USD
        
In this arbitrge deal, the CNY is called the profit currency, because we started with 6.9 CNY and after all that drama we went through, we ended up with 7.1 CNY. We use letter A to denote a profit currency. AUD is the common base currency, because AUD/USD and AUD/CNY quotes AUD (the currency before the forward slash) in terms of CNY or USD (the quote currency, the currency after the forward slash).

The reason why this arbitrage deal is profitable is because of mispricing in the market of the implicit USD/CNY exchange rate. 
What do I mean by that?
When you look at an exchange rate: USD/CNY: bid: 6.8, ask: 6.9. What it means is that in order to obtain 1 USD, you need to give up 6.9 CNY, and that if you give up 1 USD, you end up with 6.8 CNY.

But there is a twist to that. Imagine we start with 1 USD, instead of selling it into 6.8 CNY, you use that 1 USD to purchase 1 / 0.77 = 1.3 AUD. you then sell that 1.3 AUD into CNY, hitting the bid price of 5.5. Now you will end up with 5.5 * 1.3 = 7.1 CNY.

The crux of this example is that, instead of selling 1 USD directly into 6.8 CNY, you first buy AUD with that 1 USD and then sell your AUD into CNY, and somehow you end up with 7.1 CNY, more than you would get if you would have sold it directly in the USD/CNY market, in which you can only get 6.8 CNY. That is all you need to know about triangular arbitrage, essentially.

If we generalise the above example to make it more relevant to all currencies. We would have the following form.
B/A: best bid: BA bid; best ask: BA ask;
X/B: best bid: XB bid; best ask: XB ask;
X/A: best bid: XA bid; best ask: XA ask;
