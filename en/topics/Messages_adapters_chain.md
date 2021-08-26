# Adapters chain

To make it easier to create your own connections, the[S\#](StockSharpAbout.md) package includes a number of special adapters: 

| Adapter
                                                                                                    | Description
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [HeartbeatMessageAdapter](../api/StockSharp.Algo.HeartbeatMessageAdapter.html)
                             | An adapter that monitors [ConnectMessage](../api/StockSharp.Messages.ConnectMessage.html) and [DisconnectMessage](../api/StockSharp.Messages.DisconnectMessage.html) messages when the connection is dropped and on subsequent attempts to re\-establish it. Additionally, it sends a [TimeMessage](../api/StockSharp.Messages.TimeMessage.html) to the connection to simulate ping messages if the [IMessageAdapter.HeartbeatInterval](../api/StockSharp.Messages.IMessageAdapter.HeartbeatInterval.html) is set. 
 |
| [Level1DepthBuilderAdapter](../api/StockSharp.Algo.Level1DepthBuilderAdapter.html)
                         | An adapter that collects [QuoteChangeMessage](../api/StockSharp.Messages.QuoteChangeMessage.html) from [Level1ChangeMessage](../api/StockSharp.Messages.Level1ChangeMessage.html) message [MarketDataMessage.BuildMode](../api/StockSharp.Messages.MarketDataMessage.BuildMode.html) was set when subscribing and level1 message contains best buy or sell information. 
                                                                                                                                            |
| [Level1ExtendBuilderAdapter](../api/StockSharp.Algo.Level1ExtendBuilderAdapter.html)
                       | An adapter that collects [Level1ChangeMessage](../api/StockSharp.Messages.Level1ChangeMessage.html) message from [QuoteChangeMessage](../api/StockSharp.Messages.QuoteChangeMessage.html) , tick trades and candles. 
                                                                                                                                                                                                                                                                                               |
| [LookupTrackingMessageAdapter](../api/StockSharp.Algo.LookupTrackingMessageAdapter.html)
                   | An adapter that monitors subscriptions of the [SecurityLookupMessage](../api/StockSharp.Messages.SecurityLookupMessage.html) type for which the connection does not send the resulting [SubscriptionFinishedMessage](../api/StockSharp.Messages.SubscriptionFinishedMessage.html) message. In this case, this adapter independently generates the resulting message after a certain timeout. 
                                                                                                                       |
| [OrderBookIncrementMessageAdapter](../api/StockSharp.Algo.OrderBookIncrementMessageAdapter.html)
           | An adapter that collects a whole order book from incremental messages. See Order books (incremental and regular) for details [Order books (incremental and regular)](Messages_adapters_books.md).
                                                                                                                                                                                                                                                                                                                   |
| [OrderBookSortMessageAdapter](../api/StockSharp.Algo.OrderBookSortMessageAdapter.html)
                     | An adapter that automatically sorts buy and sell orders in the order book if is [QuoteChangeMessage.IsSorted](../api/StockSharp.Messages.QuoteChangeMessage.IsSorted.html) set to **false**.
                                                                                                                                                                                                                                                                                                                        |
| [OrderBookTruncateMessageAdapter](../api/StockSharp.Algo.OrderBookTruncateMessageAdapter.html)
             | An adapter that automatically cuts the order book depth if [MarketDataMessage.MaxDepth](../api/StockSharp.Messages.MarketDataMessage.MaxDepth.html) was set when subscribing.
                                                                                                                                                                                                                                                                                                                                       |
| [OrderLogMessageAdapter](../api/StockSharp.Algo.OrderLogMessageAdapter.html)
                               | An adapter that automatically creates an order book from the order log if [MarketDataMessage.BuildMode](../api/StockSharp.Messages.MarketDataMessage.BuildMode.html) was set when subscribing. See for details [Order log](Messages_adapters_orderlog.md).
                                                                                                                                                                                                                                                          |
| [PartialDownloadMessageAdapter](../api/StockSharp.Algo.PartialDownloadMessageAdapter.html)
                 | An adapter that automatically splits a history request into multiple sub\-requests at intervals. See [Historical data](Messages_adapters_history.md) for details.
                                                                                                                                                                                                                                                                                                                                                   |
| [SecurityMappingMessageAdapter](../api/StockSharp.Algo.SecurityMappingMessageAdapter.html)
                 | An adapter that automatically replaces instrument IDs, if they are specified in the [ISecurityMappingStorage](../api/StockSharp.Algo.Storages.ISecurityMappingStorage.html) storage.
                                                                                                                                                                                                                                                                                                                                |
| [SecurityNativeIdMessageAdapter](../api/StockSharp.Algo.SecurityNativeIdMessageAdapter.html)
               | An adapter that automatically replaces instrument IDs, if the adapter works with system instrument codes [IMessageAdapter.IsNativeIdentifiers](../api/StockSharp.Messages.IMessageAdapter.IsNativeIdentifiers.html).
                                                                                                                                                                                                                                                                                                |
| [SubscriptionOnlineMessageAdapter](../api/StockSharp.Algo.SubscriptionOnlineMessageAdapter.html)
           | An adapter that monitors subscriptions and prevents duplicate online subscriptions from being sent further into the connection. Duplicate subscriptions are saved and added to outgoing messages that inherit from [ISubscriptionIdMessage](../api/StockSharp.Messages.ISubscriptionIdMessage.html) via the [ISubscriptionIdMessage.SubscriptionIds](../api/StockSharp.Messages.ISubscriptionIdMessage.SubscriptionIds.html) property..
                                                                             |
| [SubscriptionMessageAdapter](../api/StockSharp.Algo.SubscriptionMessageAdapter.html)
                       | Subscription monitoring adapter. Unlike [SubscriptionOnlineMessageAdapter](../api/StockSharp.Algo.SubscriptionOnlineMessageAdapter.html), adapter redirects duplicate subscriptions further and works not only with online subscriptions, but also with history.
                                                                                                                                                                                                                                                    |
| [TransactionOrderingMessageAdapter](../api/StockSharp.Algo.TransactionOrderingMessageAdapter.html)
         | An adapter that monitors transactional messages (orders or trades) and sorts them in case the information about the trade comes earlier than the information about the order for which the trade was completed.
                                                                                                                                                                                                                                                                                                     |
| [StorageMessageAdapter](../api/StockSharp.Algo.Storages.StorageMessageAdapter.html)
                        | An adapter that monitors historical subscriptions and tries to load data from internal storage. If the required data is not available, the subscription is redirected fur
                                                                                                                                                                                                                                                                                                                                           |
| [StorageMetaInfoMessageAdapter](../api/StockSharp.Algo.Storages.StorageMetaInfoMessageAdapter.html)
        | An adapter trying to load meta data ([SecurityMessage](../api/StockSharp.Messages.SecurityMessage.html), [BoardMessage](../api/StockSharp.Messages.BoardMessage.html), [PositionChangeMessage](../api/StockSharp.Messages.PositionChangeMessage.html)) from internal storage.
                                                                                                                                                                                                                                       |
| [CandleBuilderMessageAdapter](../api/StockSharp.Algo.Candles.Compression.CandleBuilderMessageAdapter.html)
 | Adapter gluing, building (from ticks or other available data) and loading candles.
                                                                                                                                                                                                                                                                                                                                                                                                                                  |