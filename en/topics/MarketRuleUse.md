# Rules using

- **Creating a rule for the order registration condition:**

  ```cs
  private void btnBuy\_Click(object sender, RoutedEventArgs e)
  {
     var order \= new Order
     { 
         Portfolio \= Portfolio.SelectedPortfolio,
         Price \= \_instr1.BestAsk.Price,
         Security \= \_instr1,
         Volume \= 1,
         Direction \= Sides.Buy,
     };
     order
         .WhenRegistered(Connector)
         .Do(() \=\> Connector.AddInfoLog("The order was successfully registered."))
         .Once()
         .Apply(this);
      
  	\/\/ registering the order
     Connector.RegisterOrder(order);
  }
  	  	  		
  ```

  Now, when the event is triggered (the order will be registered on exchange), the action specified through the [IMarketRule.Do](../api/StockSharp.Algo.IMarketRule.Do.html) method will be called. 

  At the end of the rule creating the [MarketRuleHelper.Apply](../api/StockSharp.Algo.MarketRuleHelper.Apply.html) method is called. As long as the method is not called for the rule \- it is inactive (the handler in the [IMarketRule.Do](../api/StockSharp.Algo.IMarketRule.Do.html) will not be called). 
- **Rules creating within the strategy:**

  ```cs
  class FirstStrategy : Strategy
  {
  	...
  	
  	protected override void OnStarting()
  	{
  		\_connector
  			.WhenCandlesFinished(\_series)
  			.Do(FinishCandle)
  			.Apply(this);
  		Security
  			.WhenNewTrade(\_connector)
  			.Do(NewTrade)
  			.Apply(this);
  		base.OnStarting();
  	}
      
      ...
  }    
  	  	  		
  ```
- **Unnecessary rules removing:**

  The [IMarketRule](../api/StockSharp.Algo.IMarketRule.html) has the [Token](../api/StockSharp.Algo.IMarketRule.Token.html) \- this token is associated with the rule. For example, for the [WhenCanceled](../api/StockSharp.Algo.MarketRuleHelper.WhenCanceled.html) rule the token will be the order.

  When the rule of the successful order cancel has worked, then it is better to remove all of the other rules related to this order:

  ```cs
  var order \= this.CreateOrder(direction, (decimal) Security.GetCurrentPrice(direction), Volume);
  var ruleCanceled \= order.WhenCanceled(Connector);
  ruleCanceled
      .Do(() \=\>
      {
          this.AddInfoLog("The order was successfully cancelled.");
  	\/\/ removing all rules associated with the specified order
          Rules.RemoveRulesByToken(ruleCanceled, (IMarketRule) ruleCanceled.Token);
      })
      .Once()
      .Apply(this);
  order
      .WhenRegistered(Connector)
      .Do(() \=\> this.AddInfoLog("The order was successfully registered."))
      .Once()
      .Apply(this);
  order
      .WhenRegisterFailed(Connector)
      .Do(() \=\> this.AddInfoLog("The order was not accepted by broker."))
      .Once()
      .Apply(this);
  order
      .WhenMatched(Connector)
      .Do(() \=\> this.AddInfoLog("The order was fully matched."))
      .Once()
      .Apply(this);
  \/\/ registering the order
  RegisterOrder(order);
  	  	  		
  ```
- **Rules combination by the condition [Or](../api/StockSharp.Algo.MarketRuleHelper.Or.html) \/ [And](../api/StockSharp.Algo.MarketRuleHelper.And.html).**

  When time is over **OR** the candle is closed:

  ```cs
  CandleSeries \_series;
  TimeSpan \_holdTimeToOpen \= TimeSpan.FromMilliseconds(5000);
  ...
  \_connector
  	.WhenIntervalElapsed(\_holdTimeToOpen)
  	.Or(\_connector.WhenCandlesStarted(\_series))
  	.Do(() \=\> this.AddInfoLog("The candle is finished or time is over."))
  	.Once()
  	.Apply(this);
  	  	  		
  ```

  Or such writing format:

  ```cs
  MarketRuleHelper
  	.Or(new IMarketRule\[\] {\_connector.WhenIntervalElapsed(\_holdTimeToOpen), \_connector.WhenCandlesStarted(\_series)})
  	.Do(() \=\> this.AddInfoLog("The candle is finished or time is over."))
  	.Once()
  	.Apply(this);
  	  	  		
  ```

  When the last trade price will be higher than 135000 **AND** lower than 140000:

  ```cs
  var priceMore \= new Unit(135000m, UnitTypes.Limit);
  var priceLess \= new Unit(140000m, UnitTypes.Limit);
  				
  MarketRuleHelper
  	.And(new IMarketRule\[\] {Security.WhenLastTradePriceMore(Connector, Connector, priceMore), Security.WhenLastTradePriceLess(Connector, Connector, priceLess)})
  	.Do(() \=\> this.AddInfoLog(string.Format("The price of the last transaction is in the range from {0} to {1}", priceMore, priceLess)))
  	.Apply(this);
  	  	  		
  ```

  > [!TIP]
  > The handler in the [IMarketRule.Do](../api/StockSharp.Algo.IMarketRule.Do.html) will be called after the last rule added through the [And](../api/StockSharp.Algo.MarketRuleHelper.And.html) has worked.
- **Periodicity of the rule \- [Until](../api/StockSharp.Algo.IMarketRule.Until.html):**

  ```cs
  bool flag \= false;
  ...
  				
  Security
  	.WhenNewTrade()
  	.Do(() \=\>
  			{
  				if(...) flag \= true;
  			})
  	.Until(() \=\> flag)			
  	.Apply(this);
  	  	  		
  ```