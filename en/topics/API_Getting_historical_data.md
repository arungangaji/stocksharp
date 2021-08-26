# Getting historical data

[S\#.API](StockSharpAbout.md) provides an opportunity to receive historical candles, which can be used both for testing and for building [Indicators](Indicators.md). 

### Working with historical candles through Connector

Working with historical candles through Connector

1. To get candles through [Connector](../api/StockSharp.Algo.Connector.html) , you need to create [Connector](../api/StockSharp.Algo.Connector.html) and add the corresponding [MessageAdapter](../api/StockSharp.Messages.MessageAdapter.html) to it. How to do this using a special control, see [Connection settings window](API_UI_ConnectorWindow.md).

   You can also add the corresponding [MessageAdapter](../api/StockSharp.Messages.MessageAdapter.html) to the [Connector](../api/StockSharp.Algo.Connector.html) through the code. For example, adapter initialization for [Interactive Brokers](IB.md) is described in [Adapter initialization Interactive Brokers](IBSample.md) and looks like this:

   ```cs
   Connector Connector \= new Connector();				
   ...				
   var messageAdapter \= new InteractiveBrokersMessageAdapter(Connector.TransactionIdGenerator)
   {
   	Address \= "\<Your Address\>".To\<EndPoint\>(),
   };
   Connector.Adapter.InnerAdapters.Add(messageAdapter);
   ...	
   Connector.Connect();
   ...
   							
   ```
2. In order to get historical candles, you need to call the [SubscribeCandles](../api/StockSharp.Algo.Connector.SubscribeCandles.html) method: 

   ```cs
   ...
   var tf \= (TimeSpan)CandlesPeriods.SelectedItem;
   var series \= new CandleSeries(typeof(TimeFrameCandle), SelectedSecurity, tf);
   Connector.SubscribeCandles(SelectedSecurity, DateTime.Now.Subtract(TimeSpan.FromTicks(tf.Ticks \* 100)), DateTime.Now);
   ...
   			
   ```
3. Historical candles are passed through the [CandleSeriesProcessing](../api/StockSharp.Algo.Connector.CandleSeriesProcessing.html) event: 

   ```cs
   ...
   Connector.CandleSeriesProcessing +\= ProcessCandle;
   ...
   			
   ```
4. Candles that appear can be rendered through the [Chart](CandlesUI.md).

### Working with historical candles through MessageAdapter

Working with historical candles through MessageAdapter

1. To get candles through the [MessageAdapter](../api/StockSharp.Messages.MessageAdapter.html), you need to create the corresponding [MessageAdapter](../api/StockSharp.Messages.MessageAdapter.html).

   For example, adapter initialization for [Interactive Brokers](IB.md) is described in [Adapter initialization Interactive Brokers](IBSample.md) and looks like this:

   ```cs
   		
   ...         
   var messageAdapter \= new InteractiveBrokersMessageAdapter(Connector.TransactionIdGenerator)
   {
   	Address \= "\<Your Address\>".To\<EndPoint\>(),
   };
   ...
   							
   ```
2. We wrap the [Interactive Brokers](IB.md) adapter in the [SecurityNativeIdMessageAdapter](../api/StockSharp.Algo.SecurityNativeIdMessageAdapter.html). security system identifier adapter. This is necessary if the trading system works with numeric or any other security identifiers other than the usual string representation.

   ```cs
   	
   ...
   SecurityNativeIdMessageAdapter \_securityAdapter;
   if (adapter.IsNativeIdentifiers)
   	\_securityAdapter \= new SecurityNativeIdMessageAdapter(adapter, new InMemoryNativeIdStorage());
   var securities \= \_securityAdapter.GetSecurities(new SecurityLookupMessage
   {
   	SecurityId \= new SecurityId
   	{
   		SecurityCode \= "EUR"
   	}
   });
   SecurityMessage eurUsd \= null;
   foreach (var security in securities)
   {
   	if (security.SecurityId.SecurityCode.CompareIgnoreCase("EURUSD"))
   		eurUsd \= security;
   }
   ...
   							
   ```
3. Now, using the received security identifier, we get candles from the adapter: 

   ```cs
   ...
   var candles \= adapter.GetCandles(eurUsd.SecurityId, TimeSpan.FromDays(1), DateTimeOffset.Now.AddDays(\-100), DateTimeOffset.Now);
   foreach (var candle in candles)
   {
   	Console.WriteLine(candle);
   }
   ...
   			
   ```

## Recommended content

[Candles](Candles.md)