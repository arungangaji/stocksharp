# На истории с Финам

Для тестирования на истории в классе [HistoryEmulationConnector](xref:StockSharp.Algo.Testing.HistoryEmulationConnector), наряду с использованием хранилища данных [IStorageRegistry](xref:StockSharp.Algo.Storages.IStorageRegistry), предусмотрен альтернативный механизм работы с источниками данных. Этот механизм позволяет "напрямую" загружать данные с серверов поставщиков исторической информации, в частности с сервера Финам или же работать с собственными источниками данных. 

Рассмотрим работу этого механизма на примере получения данных с сервиса Финам. Для работы с Финам в [S\#](StockSharpAbout.md) существует специальный класс [FinamMessageAdapter](xref:StockSharp.Finam.FinamMessageAdapter), который позволяет получать свечи, тики и информацию об инструментах. 

## Тестирование с данными, загруженными с Финама

1. Сначала нужно получить информацию об инструментах с сервиса Финам. Для этого необходимо создать хранилище для инструментов (**FinamSecurityStorage**) \- класс, реализующий интерфейс [ISecurityStorage](xref:StockSharp.Algo.Storages.ISecurityStorage). Код такого класса есть в примере *Samples\/Testing\/SampleHistoryTesting*. 
   1. Создаем инструмент.

      ```none
      var security = new Security
      {
          Id = secid,
          Code = secCode,
          Board = board
      };
       
      ```
   2. Создаем экземпляр класса загрузчика данных с Финама:

      ```none
      // удаляем старый адаптер маркет-данных и добавляем новый от Финам
      connector.Adapter.InnerAdapters.Remove(connector.MarketDataAdapter);
      connector.Adapter.InnerAdapters.Add(new CustomHistoryMessageAdapter(new FinamMessageAdapter(connector.TransactionIdGenerator)));
      ```
