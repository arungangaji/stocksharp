# Хранилище маркет\-данных

Хранилище исторических данных предназначено для загрузки маркет\-данных (инструменты, свечи, тиковые сделки и стаканы) из различных источников и хранения их в локальном или удаленном хранилище. [S\#.Designer](Designer.md) может использовать источники как исторические (например, Finam), так и данных реального времени (например, подключение к Quik или SmartCOM для получения стаканов). В дальнейшем сохраненная информация доступна для использования торговыми стратегиями.

Для открытия вкладки **Маркет\-данные** необходимо перейти на вкладку **Общее** и нажать кнопку **Маркет\-данные**. Вкладка **Маркет\-данные** разделена на три зоны. В зоне слева представлен список всех полученных инструментов, из всех источников, которые когда\-либо были подключены. В зоне по центру активные инструменты. По этим инструментам можно скачать или просмотреть скачанную историю. В зоне справа отображаются имеющиеся данные по инструменту, выбранному в центральной зоне, а также можно скачать данные по выбранному инструменту.

![Designer Repository of historical data 00](~/images/Designer_Repository_of_historical_data_00.png)

Для просмотра имеющихся данных необходимо выбрать инструмент в списке **Активные**. На панели справа необходимо выбрать хранилище исторических данных или создать его если оно не было создано ([Создание хранилища исторических данных](Designer_Creating_repository_of_historical_data.md)). После чего отобразятся все имеющиеся данные в хранилище по выбранному инструменту инструменту.

## См. также

[Создание хранилища исторических данных](Designer_Creating_repository_of_historical_data.md)