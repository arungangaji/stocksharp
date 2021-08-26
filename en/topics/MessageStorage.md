# Messages storage

Along with the use of trading object storages, you can use message storages. Work with these storages is also carried out through the [IMarketDataStorage\`1](../api/StockSharp.Algo.Storages.IMarketDataStorage`1.html). interface. For example, to work with candles, you can use the storage of the IMarketDataStorage\<CandleMessage\> type. [IStorageRegistry](../api/StockSharp.Algo.Storages.IStorageRegistry.html) also contains a set of methods for obtaining the required message storages. So, the time candle storage can be obtained, as shown in the following code snippet. 

```cs
   var security \= new Security() { Id \= "ESM5@NYSE" };
   var candleMessageStorage \= \_storage.GetCandleMessageStorage(typeof(TimeFrameCandleMessage), security, TimeSpan.FromMinutes(1));
	
```

Then you can work with the storage using [IMarketDataStorage.Load](../api/StockSharp.Algo.Storages.IMarketDataStorage.Load.html) and\/or [IMarketDataStorage.Save](../api/StockSharp.Algo.Storages.IMarketDataStorage.Save.html) methods, as shown in the example in the [API](StoragesApi.md). 

Note that [S\#](StockSharpAbout.md) allows you to convert the trading object storage types to the corresponding types of message storages and vice versa. For example, IMarketDataStorage\<MarketDepth\> can be converted to the IMarketDataStorage\<QuoteChangeMessage\> type and vice versa. 

```cs
	
   var security \= new Security() { Id \= "ESM5@NYSE" };
   
   var depthStorage \= \_storage.GetMarketDepthStorage(\_security);
   var quoteMessageStorage \= depthStorage as IMarketDataStorage\<QuoteChangeMessage\>;
   
   var quoteMessageStorage1 \= \_storage.GetQuoteMessageStorage(\_security);
   var depthStorage1 \= quoteMessageStorage1 as IMarketDataStorage\<MarketDepth\>;
	
```

It should pay attention to the relevance of using the message storage to store own orders and trades. The matter is that for these trading objects there are no corresponding storages. In this case, you must use the IMarketDataStorage\<ExecutionMessage\> message storage. The following example shows how to store own trades in the storage. 

### Example of saving own trades

Example of saving own trades

1. 1. First, an instance of the connector is created, as well as a storage. In addition, we specify the identifier of the instrument with which we will work and declare a variable for the transaction storage. The transaction storage itself for the specified instrument will be received in the instrument getting event using the [IMessageStorageRegistry.GetTransactionStorage](../api/StockSharp.Algo.Storages.IMessageStorageRegistry.GetTransactionStorage.html) method. 

   ```cs
   var connector \= new Connector();
   var storagePath \= @"....";
   var securityId \= "RIM5@FORTS";
   var storage \= new StorageRegistry() { DefaultDrive \= new LocalMarketDataDrive(storagePath) };
   IMarketDataStorage\<ExecutionMessage\> tranStorage \= null;
   connector.NewSecurity +\= security \=\>
   {
   		if (security.Id \=\= securityId)
   			tranStorage \= storage.GetTransactionStorage(security.ToSecurityId());
   };
    
   ```
2. Saving own trades will be performed in the [Connector.NewMyTrade](../api/StockSharp.Algo.Connector.NewMyTrade.html) event handler using the [IMarketDataStorage.Save](../api/StockSharp.Algo.Storages.IMarketDataStorage.Save.html). method. Before saving, the list of own trades is converted to the IEnumerable\<ExecutionMessage\> type. The procedure for order registering itself in this example is omitted. 

   ```cs
   connector.NewMyTrade +\= trade \=\>
   {
       tranStorage.Save(new\[\] {trade.ToMessage()});
   };
   ```

## Recommended content

[Api](StoragesApi.md)