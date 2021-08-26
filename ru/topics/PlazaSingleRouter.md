# Один логин \- несколько роботов

Роутер [Plaza II](Plaza.md) позволяет одновременно подключаться нескольким роботам. Для этого необходимо, чтобы каждое из подключений имело уникальное имя. Имя для подключения задаётся через свойство [AppName](../api/StockSharp.Plaza.PlazaMessageAdapter.AppName.html)

```cs
var messageAdapter \= new PlazaMessageAdapter(Connector.TransactionIdGenerator)
{
    Login \= "\<Your Login\>",
    Password \= "\<Your Password\>".To\<SecureString\>(),
    Address \= SmartComAddresses.Demo,
    AppName \= "robot\_PRADA",
};      
      
```

## См. также