# Основные алгоритмы

Наравне с [Котирование](StrategyQuoting.md) в [S\#](StockSharpAbout.md) добавлен класс [TraderHelper](../api/StockSharp.Algo.TraderHelper.html), в который входят различные методы простых торговых алгоритмов:

1. Очистить стакан от собственных заявок через метод [GetFilteredQuotes](../api/StockSharp.Algo.TraderHelper.GetFilteredQuotes.html) (чтобы выставлять заявки относительно других участников рынка, и предотвратить борьбу своих роботов друг с другом):

   ```cs
   \/\/ любой инструмент
   var someSecurity \= \_connector.Securities.First();
   var someOrders \= new List\<Order\>();
   \/\/ заполняем коллекцию собственными заявками
   \/\/ вычисляем истинно\-лучшую цену на покупку
   Console.WriteLine(\_connector.GetMarketDepth(someSecurity).GetFilteredQuotes(Sides.Buy, someOrders, null).Max(q \=\> q.Price));
   ```
2. Обрезать цену через метод [ShrinkPrice](../api/StockSharp.Algo.TraderHelper.ShrinkPrice.html), чтобы она стала кратной шагу цены, и торговая система приняла заявку:

   ```cs
   \/\/ любой инструмент
   var someSecurity \= \_connector.Securities.First();
   Console.WriteLine(someSecurity.ShrinkPrice(13453.65342));
   ```
3. Получить позицию по совершенным сделкам через метод [GetPosition](../api/Overload:StockSharp.Algo.TraderHelper.GetPosition.html):

   ```cs
   Console.WriteLine(\_connector.GetPosition(Portfolio,Security, clientCode, depoName);
   ```
4. Проверить, является ли текущее время торгуемым (не закончилась ли сессия, не начался ли клиринг) через метод [IsTradeTime](../api/Overload:StockSharp.Algo.TraderHelper.IsTradeTime.html): 

   ```cs
   \/\/ любой инструмент
   var someSecurity \= \_connector.Securities.First();
   Console.WriteLine(someSecurity.Board.IsTradeTime(currentTime));
   ```
5. Остальные методы класса [TraderHelper](../api/StockSharp.Algo.TraderHelper.html) описываются в разделах [Снятие заявок](OrdersCancel.md) и [Замена заявок](OrdersReRegister.md). 

## См. также

[Котирование](StrategyQuoting.md)

[Снятие заявок](OrdersCancel.md)

[Замена заявок](OrdersReRegister.md)