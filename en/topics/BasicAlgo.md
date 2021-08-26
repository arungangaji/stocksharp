# Base algorithms

Along with [Quoting](StrategyQuoting.md), the [S\#](StockSharpAbout.md) contains the [TraderHelper](../api/StockSharp.Algo.TraderHelper.html) class, which includes a variety of simple trading algorithms methods:

1. To clear the order book from its own orders through the [GetFilteredQuotes](../api/StockSharp.Algo.TraderHelper.GetFilteredQuotes.html) method (to register the orders in relation to other market players and to prevent own algorithms to fight each other):

   ```cs
   \/\/ the sample security
   var someSecurity \= \_connector.Securities.First();
   var someOrders \= new List\<Order\>();
   \/\/ fill the collection by own orders
   \/\/ to get the best big price
   Console.WriteLine(\_connector.GetMarketDepth(someSecurity).GetFilteredQuotes(Sides.Buy, someOrders, null).Max(q \=\> q.Price));
   ```
2. To adjust the price through the [ShrinkPrice](../api/StockSharp.Algo.TraderHelper.ShrinkPrice.html) method, so it become a multiple of price increment and trading system accepts the order:

   ```cs
   \/\/ the sample security
   var someSecurity \= \_connector.Securities.First();
   Console.WriteLine(someSecurity.ShrinkPrice(13453.65342));
   ```
3. To get the position on closed trades through the [GetPosition](../api/Overload:StockSharp.Algo.TraderHelper.GetPosition.html) method:

   ```cs
   Console.WriteLine(\_connector.GetPosition(Portfolio,Security, clientCode, depoName);
   ```
4. To check whether the current time traded (is session closed? is clearing started?) through the [IsTradeTime](../api/Overload:StockSharp.Algo.TraderHelper.IsTradeTime.html) method: 

   ```cs
   \/\/ the sample security
   var someSecurity \= \_connector.Securities.First();
   Console.WriteLine(someSecurity.Board.IsTradeTime(currentTime));
   ```
5. The rest of the [TraderHelper](../api/StockSharp.Algo.TraderHelper.html) class methods are described in the [Order cancel](OrdersCancel.md) and [Order replace](OrdersReRegister.md) sections. 

## Recommended content

[Quoting](StrategyQuoting.md)

[Order cancel](OrdersCancel.md)

[Order replace](OrdersReRegister.md)