# Коннекторы

Для работы с биржами и источниками данных в [S\#](StockSharpAbout.md) рекомендуется работать через базовый класс [Connector](../api/StockSharp.Algo.Connector.html). 

Рассмотрим работу с [Connector](../api/StockSharp.Algo.Connector.html). Исходные коды примера находятся в проекте Samples\/Common\/SampleConnection.

![multiconnection main](~/images/multiconnection_main.png)

Создаём экземпляр класса [Connector](../api/StockSharp.Algo.Connector.html):

```cs
...
public Connector Connector;
...
public MainWindow()
{
	InitializeComponent();
	Connector \= new Connector();
	InitConnector();
}
		
```

Для конфигурирования [Connector](../api/StockSharp.Algo.Connector.html) у **S\#.API** есть специальный графический интерфейс, в котором можно настроить сразу несколько подключений одновременно. Как им воспользоваться описано в пункте [Графическое конфигурирование](API_ConnectorsUIConfiguration.md). 

```cs
...
private const string \_connectorFile \= "ConnectorFile";
...
private void Setting\_Click(object sender, RoutedEventArgs e)
{
	if (Connector.Configure(this))
	{
		new XmlSerializer\<SettingsStorage\>().Serialize(Connector.Save(), \_connectorFile);
	}
}
	  				
```

![API GUI ConnectorWindow](~/images/API_GUI_ConnectorWindow.png)

Аналогично можно добавлять подключения напрямую из кода (без графических окон), воспользовавшись методом расширением [TraderHelper.AddAdapter\`\`1](../api/StockSharp.Algo.TraderHelper.AddAdapter``1.html):

```cs
...
\/\/ добавляем два подключения к QUIK (цены и заявки)
connector.AddAdapter\<LuaFixMarketDataMessageAdapter\>(a \=\> { });
connector.AddAdapter\<LuaFixTransactionMessageAdapter\>(a \=\> { });
	  				
```

В один объект [Connector](../api/StockSharp.Algo.Connector.html) можно добавлять неограниченное количество подключений. Поэтому одновременно из программы можно подключаться сразу к нескольким биржам и брокерам.

В методе *InitConnector* устанавливаем требуемые обработчики событий [IConnector](../api/StockSharp.BusinessEntities.IConnector.html):

```cs
private void InitConnector()
{
	\/\/ subscribe on connection successfully event
	Connector.Connected +\= () \=\>
	{
		this.GuiAsync(() \=\> ChangeConnectStatus(true));
	};
	\/\/ subscribe on connection error event
	Connector.ConnectionError +\= error \=\> this.GuiAsync(() \=\>
	{
		ChangeConnectStatus(false);
		MessageBox.Show(this, error.ToString(), LocalizedStrings.Str2959);
	});
	Connector.Disconnected +\= () \=\> this.GuiAsync(() \=\> ChangeConnectStatus(false));
	\/\/ subscribe on error event
	Connector.Error +\= error \=\>
		this.GuiAsync(() \=\> MessageBox.Show(this, error.ToString(), LocalizedStrings.Str2955));
	\/\/ subscribe on error of market data subscription event
	Connector.MarketDataSubscriptionFailed +\= (security, msg, error) \=\>
		this.GuiAsync(() \=\> MessageBox.Show(this, error.ToString(), LocalizedStrings.Str2956Params.Put(msg.DataType, security)))
	Connector.NewSecurity +\= \_securitiesWindow.SecurityPicker.Securities.Add;
	Connector.NewTrade +\= \_tradesWindow.TradeGrid.Trades.Add;
	Connector.NewOrder +\= \_ordersWindow.OrderGrid.Orders.Add;
	Connector.NewStopOrder +\= \_stopOrdersWindow.OrderGrid.Orders.Add;
	Connector.NewMyTrade +\= \_myTradesWindow.TradeGrid.Trades.Add;
	
	Connector.NewPortfolio +\= \_portfoliosWindow.PortfolioGrid.Portfolios.Add;
	Connector.NewPosition +\= \_portfoliosWindow.PortfolioGrid.Positions.Add;
	\/\/ subscribe on error of order registration event
	Connector.OrderRegisterFailed +\= \_ordersWindow.OrderGrid.AddRegistrationFail;
	\/\/ subscribe on error of order cancelling event
	Connector.OrderCancelFailed +\= OrderFailed;
	\/\/ subscribe on error of stop\-order registration event
	Connector.OrderRegisterFailed +\= \_stopOrdersWindow.OrderGrid.AddRegistrationFail;
	\/\/ subscribe on error of stop\-order cancelling event
	Connector.StopOrderCancelFailed +\= OrderFailed;
	\/\/ set market data provider
	\_securitiesWindow.SecurityPicker.MarketDataProvider \= Connector;
	try
	{
		if (File.Exists(\_settingsFile))
		{
			var ctx \= new ContinueOnExceptionContext();
			ctx.Error +\= ex \=\> ex.LogError();
			using (new Scope\<ContinueOnExceptionContext\> (ctx))
				Connector.Load(new XmlSerializer\<SettingsStorage\>().Deserialize(\_settingsFile));
		}
	}
	catch
	{
	}
	ConfigManager.RegisterService\<IExchangeInfoProvider\>(new InMemoryExchangeInfoProvider());
	
	\/\/ нужен для графического конфигурирования
	ConfigManager.RegisterService\<IMessageAdapterProvider\>(new FullInMemoryMessageAdapterProvider(Connector.Adapter.InnerAdapters));
}
```

Как сохранять и загружать настройки [Connector](../api/StockSharp.Algo.Connector.html) в файл можно ознакомиться в пункте [Сохранение и загрузка настроек](API_Connectors_SaveConnectorSettings.md).

О создании собственного [Connector](../api/StockSharp.Algo.Connector.html) можно ознакомиться в пункте [Создание собственного коннектора](ConnectorCreating.md).

Выставление заявок описаны в пунктах [Заявки](Orders.md), [Создать новую заявку](CreateNewOrder.md), [Создать новую стоп заявку](API_StopOrders.md). 

## См. также

[Графическое конфигурирование](API_ConnectorsUIConfiguration.md)