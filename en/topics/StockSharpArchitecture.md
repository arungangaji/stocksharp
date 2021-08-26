# Architecture S\#.API

[S\#.API](StockSharpAbout.md) \- a free library for beginners and professionals in the field of algorithmic trading. [S\#.API](StockSharpAbout.md) is focused on [C\#](https://en.wikipedia.org/wiki/C_Sharp_(programming_language)) language programming. 

1. Quickly (a few hours) and reliably to move from one connection to another (for example, from 

   [Interactive Brokers](IB.md)

    to 

   [OpenECry](OEC.md)

   ). 
2. There is no need to rewrite the trading algorithm after the release of a new version of the gateway to the broker. 

   [S\#.API](StockSharpAbout.md)

    updated regularly \- see 

   [Releases History](https://github.com/stocksharp/stocksharp/blob/master/_ReleaseNotes/CHANGE_LOG_API.md)

   . 
3. Algorithm code has a unified format (HFT or position trading). 
4. Big community unites different algorithmic traders, regardless of board, broker or connection type. 
5. The increase of customers for trading strategies developers. 

![ssapi schema](~/images/ssapi_schema.png)

The library is divided into the following main components:

- [BusinessEntities](../api/StockSharp.BusinessEntities.html)

   \- basic trading objects (instrument, order, trade, etc.), including the interface 

  [IConnector](../api/StockSharp.BusinessEntities.IConnector.html)

   description. 
- [Algo](../api/StockSharp.Algo.html)

   \- combines a large number of modules that are directly related to trading strategies writing (for more details see 

  [Trading strategies](Strategy.md)

  ). There are some auxiliary strategies, such as market making under several schemes (for more details see 

  [Quoting](StrategyQuoting.md)

  ) in this component. Also there is the base implementation of 

  [IConnector](../api/StockSharp.BusinessEntities.IConnector.html)

   interface \- Connector class in this component. 
  - [Strategies](../api/StockSharp.Algo.Strategies.html) \- the base classes for creating strategies.
  - [Candles](../api/StockSharp.Algo.Candles.html) \- here is all the necessary functionality to work with candles and graphic patterns recognition collected (for more details see [Candles](Candles.md)).
  - [Indicators](../api/StockSharp.Algo.Indicators.html) \- contains the base classes and interfaces for creating technical indicators, as well as built\-in indicators. See [Indicators](Indicators.md).
  - [Derivatives](../api/StockSharp.Algo.Derivatives.html) \- classes for work with options. See [Options](Options.md).
  - [Testing](../api/StockSharp.Algo.Testing.html) \- classes for different types of strategies testing: on random and historical data, on actual market data and also for optimization. See [Testing](StrategyTesting.md).
  - [Storages](../api/StockSharp.Algo.Storages.html) \- classes for working with data storage. See [Market\-Data storage](Storages.md).
  - **Other modules** \- various additional modules associated with strategies development: commissions, slippages, profit\-loss, risk management, statistics, a number of auxiliary algorithms (order book cleaning from own orders, the calculation of the market price, rounding prices to the instrument tick price, etc.) and so on, that simplify the creation of trading algorithms.
- [Messages](../api/StockSharp.Messages.html)

   \- message classes, main enumerations, exchanges hours of operation, the Unit 

  [Unit](../api/StockSharp.Messages.Unit.html)

   class, etc. 
- [Xaml](../api/StockSharp.Xaml.html)

   \- graphical components for tabular information display (orders, trades, Level1, etc.), instruments search, portfolios, order book display, options board, strategies performance monitoring, logging (and others), including: 
  - [Charting](../api/StockSharp.Xaml.Charting.html) \- tools for creating various diagrams: candles, indicators, profitability, etc.
  - [Diagram](../api/StockSharp.Xaml.Diagram.html) \- graphical elements for strategies visual creation.
- [Logging](../api/StockSharp.Logging.html)

   \- special tools to work with debug information. There are different ways to output debug messages: to the debug window, to a file, to the graphical component, send via email or sound beep in case of problems in the algorithm. 
- **Connectors modules**

   \- include the connectors implementation to the trading systems with the same names (for example, 

  [InteractiveBrokers](../api/StockSharp.InteractiveBrokers.html)

   contains the connector implementation to 

  [Interactive Brokers](IB.md)

  ). 