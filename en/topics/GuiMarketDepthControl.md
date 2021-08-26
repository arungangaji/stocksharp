# Order book

![GUI MarketDepthControl](~/images/GUI_MarketDepthControl.png)

[MarketDepthControl](../api/StockSharp.Xaml.MarketDepthControl.html) \- is a graphical component for displaying an order book. The component allows you to display quotes and own orders. 

**Main properties and methods**

- [MaxDepth](../api/StockSharp.Xaml.MarketDepthControl.MaxDepth.html) \- the depth of an order book.
- [IsBidsOnTop](../api/StockSharp.Xaml.MarketDepthControl.IsBidsOnTop.html) \- to display purchases on top.
- [UpdateFormat](../api/StockSharp.Xaml.MarketDepthControl.UpdateFormat.html) \- to update the format for displaying prices and volumes using the instrument.
- [ProcessOrder](../api/StockSharp.Xaml.MarketDepthControl.ProcessOrder.html) \- to process an order.
- [UpdateDepth](../api/StockSharp.Xaml.MarketDepthControl.UpdateDepth.html) \- to refresh an order book.
- [UpdateDepth](../api/StockSharp.Xaml.MarketDepthControl.UpdateDepth.html) \- to refresh an order book with a message.

Below is the code snippet with its use. The code example is taken from *Samples\/BarChart\/SampleBarChart*. 

```xaml
\<Window x:Class\="SampleBarChart.QuotesWindow"
    xmlns\="http:\/\/schemas.microsoft.com\/winfx\/2006\/xaml\/presentation"
    xmlns:x\="http:\/\/schemas.microsoft.com\/winfx\/2006\/xaml"
    xmlns:xaml\="http:\/\/schemas.stocksharp.com\/xaml"
    Title\="QuotesWindow" Height\="600" Width\="280"\>
	\<xaml:MarketDepthControl x:Name\="DepthCtrl" x:FieldModifier\="public" \/\>
\<\/Window\>
	  				
```
```cs
private void ConnectorOnMarketDepthsChanged(IEnumerable\<MarketDepth\> depths)
{
	foreach (var depth in depths)
	{
		var wnd \= \_quotesWindows.TryGetValue(depth.Security);
		if (wnd \!\= null)
			wnd.DepthCtrl.UpdateDepth(depth);
	}
}
	  				
```