# Создание свечей по корзине инструментов

Для создания свечей [ContinuousSecurity](../api/StockSharp.Algo.ContinuousSecurity.html), [WeightedIndexSecurity](../api/StockSharp.Algo.WeightedIndexSecurity.html) или [ExpressionIndexSecurity](../api/StockSharp.Algo.Expressions.ExpressionIndexSecurity.html) используется тот же механизм, что и при создании свечей [Security](../api/StockSharp.BusinessEntities.Security.html).

Например создадим 1мин. свечи для спреда GZM5 \- LKM5:

```cs
private Connector \_connector;
private Security \_instr1;
private Security \_instr2;
private WeightedIndexSecurity \_indexInstr;
private const string \_secCode1 \= "GZM5";
private const string \_secCode2 \= "LKM5";
private CandleSeries \_indexSeries;
readonly TimeSpan \_timeFrame \= TimeSpan.FromMinutes(1);
private ChartArea \_area;
private ChartCandleElement \_candlesElem;
...
if (\_connector.Configure(this))
			{
				new XmlSerializer\<SettingsStorage\>().Serialize(\_connector.Save(), \_connectorFile);
			}
			
...
\_area \= new ChartArea();
\_chart.Areas.Add(\_area);
\_candlesElem \= new ChartCandleElement();
\_area.Candles.Add(\_candlesElem);
...
\_connector.CandleSeriesProcessing +\= Connector\_CandleSeriesProcessing;
....
ConfigManager.RegisterService\<ISecurityProvider\>(\_connector);
ConfigManager.RegisterService\<ICompilerService\>(new RoslynCompilerService());
...
\_indexInstr \= new WeightedIndexSecurity() { Board \= ExchangeBoard.Nyse, Id \= "IndexInstr" };
\_indexInstr.Weights.Add(\_instr1, 1);
\_indexInstr.Weights.Add(\_instr2, \-1);
\_indexSeries \=
	new CandleSeries(typeof(TimeFrameCandle), \_indexInstr, \_timeFrame)
	{
		BuildCandlesMode \= MarketDataBuildModes.Build,
		BuildCandlesFrom \= MarketDataTypes.Trades,
	};
...
\_connector.SubscribeCandles(\_indexSeries, DateTime.Today.Subtract(TimeSpan.FromDays(30)), DateTime.Now);			
		
```

После этого в обработчик события [Connector.CandleSeriesProcessing](../api/StockSharp.Algo.Connector.CandleSeriesProcessing.html) \- DrawCandles, будут поступать свечи, которые можно вывести на график:

```cs
private void Connector\_CandleSeriesProcessing(CandleSeries candleSeries, Candle candle)
{
    if (candleSeries \=\= \_indexSeries) 
       {
          var chartData \= new ChartDrawData();
          chartData.Group(candle.OpenTime).Add(\_candleElement, candle);
          \_chart.Draw(chartData);
       }
}
		
```

## См. также

[Непрерывный фьючерс](SecurityContinuous.md)

[Индекс](SecurityIndex.md)