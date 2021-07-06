# Binance-Triangular-Arbitrage
This web application screens for triangular arbitrage opportunities on Binance and present it in the UI. You may also toggle the auto trade button to let the underlying code execute trades for you.

== Basics of triangular arbitrage you should know ==

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

, where A, B and X are currency symbols. The currency before the forward slash is the base currency and the one after the forward slash is the quote currency. For instance: BA bid donotes how many units of currency A you can get by giving up one unit of currency B, and BA ask denotes how many units of currency A you need to give up in order to get one unit of currency B.

There are TWO so called "directions" to a triangular arbitrage deal.
One direction is: A --BUY--> B --BUY--> X --SELL--> A;
For this direction to be profitable, you must have the following inequality hold true:
            (XA bid / XB ask) / BA ask - 1 > 0
In the source code, I name the term (XA bid / XB ask) "m1", and the term BA ask "n1".
So the inequality can be re-written as m1/n1 - 1 > 0.

The other direction is: A --BUY--> X --SELL--> B --SELL--> A;
For this direction to be profitable, you must have
            BA bid / (XA ask / XB bid) - 1 > 0
If you swap BA bid for n2 and (XA ask / XB bid) for m2, you have:
            n2 / m2 - 1 > 0

Using easy algebra, you can prove that when m1/n1 - 1 > 0, it must be that n2 / m2 - 1 < 0, and vice versa.
Namely, you cannot have both direction of triangular arbitrage to be profitable at the same time.
However, you should note that the reverse does not necessarily hold true. i.e., n2 / m2 - 1 < 0 does not necessarily mean m1 / n1 - 1 > 0.
This says that it could be the case that both directions are not profitable.


== Functions of this application ==

This application is an HTML file with JavaScript code directly embeded in it. It screens all trrading cryptos on the Binance exchange and presents the currency pairs that can potentially be used in a triangular arbitrage trade and present it to the UI. You can also toggle on the auto trading button to stop the UI refresh and hand all your arbitrage trade over to your computer.

As I have said, there are two modes of trading. You can either trade by yourself whenever you deem the profit margin of a trade to be satisfactory, or you can set a threshold level of profit margin at which you would like to execute the trade, and let your computer do it for you.

The profit margin is as close to what you can get as possible, in that it takes into account the maximum possible commission rate Binance charges (0.1% per trade).

You can adapt the code to make it work on other exchanges if you are so inclined.

Have fun.

