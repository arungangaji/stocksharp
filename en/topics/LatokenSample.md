# Adapter initialization Latoken

The code below demonstrates how to initialize the [LatokenMessageAdapter](../api/StockSharp.LATOKEN.LatokenMessageAdapter.html) and send it to [Connector](../api/StockSharp.Algo.Connector.html).

```cs
            Connector Connector \= new Connector();				
            ...				
            var messageAdapter \= new LatokenMessageAdapter(Connector.TransactionIdGenerator)
            {
                Key \= "\<Your API Key\>".To\<SecureString\>(),
                Secret \= "\<Your API Secret\>".To\<SecureString\>(),
            };
            Connector.Adapter.InnerAdapters.Add(messageAdapter);
            ...	
							
```

## Recommended content

[Connection settings window](API_UI_ConnectorWindow.md)