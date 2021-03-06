# Исполнение стратегий на сервере

Стратегии, созданные в [S\#.Designer](Designer.md), можно запускать в [S\#.Shell](Shell.md). [S\#.Shell](Shell.md) быстрее и меньше занимает памяти, чем [S\#.Designer](Designer.md), и поэтому стратегии будут иметь лучше производительность. Такой подход идеален для размещения стратегий на сервере.

[S\#.Shell](Shell.md) может выступать как сервер\-контейнер для разного типа стратегий, в том числе и созданных в [S\#.Designer](Designer.md).

Для запуска стратегии в [S\#.Shell](Shell.md) необходимо экспортировать стратегию в файл как описано в пункте [Экспорт стратегий](Designer_Export_strategies.md) или [Экспорт стратегий с шифрованием](Designer_Encryption.md) и загрузить ее в [S\#.Shell](Shell.md) как описано в пункте [Запуск стратегии созданной в S\#.Designer](Shell_run_Designer_strategy.md).

## См. также

[RemoteManager](Shell_RemoteManager.md)
