# Создать новую стоп заявку

Для создания новой стоп заявки необходимо создать объект [Order](../api/StockSharp.BusinessEntities.Order.html), который содержит информацию о заявке и зарегистрировать его на бирже.

В отличии от обычной заявки для стоп заявки необходимо указать свойство [Order.Type](../api/StockSharp.BusinessEntities.Order.Type.html) как [Conditional](../api/StockSharp.Messages.OrderTypes.Conditional.html) и задать свойство [Order.Condition](../api/StockSharp.BusinessEntities.Order.Condition.html) с необходимыми условиями заявки.

В дальнейшем, если требуется работа с заявкой (например, отменить ее или изменить), то необходимо использовать именно этот объект [Order](../api/StockSharp.BusinessEntities.Order.html). Для регистрации заявок на бирже предусмотрен метод [RegisterOrder](../api/StockSharp.Algo.Connector.RegisterOrder.html) который отправляет заявку на сервер.

```cs
Connector Connector \= new Connector();		
...   
private void StopOrder\_Click(object sender, RoutedEventArgs e)
{
	var order \= new Order
	{
		Security \= SecurityEditor.SelectedSecurity,
		Portfolio \= PortfolioEditor.SelectedPortfolio,
		Price \= decimal.Parse(TextBoxPrice.Text),
		Volume \= decimal.Parse(TextBoxVolumePrice.Text),
		Direction \= Sides.Buy,
        Type \= OrderTypes.Conditional,
        Condition \= new QuikOrderCondition()
        {
            Type \= QuikOrderConditionTypes.StopLimit,
            StopLimitPrice \= decimal.Parse(TextBoxStopLimitPrice.Text),
        }
	};
	Connector.RegisterOrder(order);
}
...
							
```

Для каждого подключения есть собственная реализация класса [OrderCondition](../api/StockSharp.Messages.OrderCondition.html) так как каждое подключение имеет свои уникальные особенности. Например, для [QUIK](Quik.md) это [QuikOrderCondition](../api/StockSharp.Quik.QuikOrderCondition.html) , для [KuCoin](Kucoin.md) это [KucoinOrderCondition](../api/StockSharp.Kucoin.KucoinOrderCondition.html) и т. д. 

## См. также

[Получение информации по заявкам](OrdersEvents.md)