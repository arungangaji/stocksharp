# Панель Схемы

Чтобы открыть панель **Схемы** необходимо нажать на кнопку **Схемы** во вкладке **Общие**. Панель **Схемы** содержит дерево скриптов, сгруппированных в папки по назначению. Схемы стратегий и составных элементов ничем не отличаются. Для их редактирования используется один общий редактор [Дизайнер стратегии](Designer_Designer_schemes_strategies_and_component_elements.md). Но, чтобы не возникало путаницы между ними, они разделены на две независимых списка и хранятся в различных папках (стратегии в папке **Стратегии**, составные элементы в папке **Составные элементы**). Выбор схемы для редактирования осуществляется двойным кликом мышки по нужному элементу в списке. При этом выбранная схема откроется в дизайнере для просмотра и редактирования. Ниже приведено описание папок панели **Схемы**:

![Designer Panel Circuits 00](~/images/Designer_Panel_Circuits_00.png)

1. Папка **Составные элементы** содержит элементы, которые представляют собой законченный функционал и могут быть использованы в различных схемах или одной схеме множество раз с различными значениями свойств. Подобные наборы элементов можно вынести в отдельный составной элемент, который дальше будет использоваться как любой обычный элемент. **Составной элемент** представляет собой обычную схему, которая сохраняется\/загружается\/редактируется как любая схема стратегии. Добавить новый составной элемент можно нажав на кнопку **Добавить**![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) во вкладке **Общие** и выбрать **Составной элемент**. Или нажав правой кнопкой мыши на папке **Составные элементы** панели **Схемы**, и нажать на кнопку **Добавить**![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) в выпавшем меню. При добавлении новых составных элементов, они автоматически добавляются в **Палитру элементов**, в группу **Составные элементы** и могут использоваться при создании других схем стратегий и составных элементов. Подробно о **Составных элементах** описано в пункте [Создание составных элементов](Designer_Creating_composite_elements.md). 

2. Папка **Стратегии** содержит стратегии, которые представляют собой схему из набора элементов и связей между ними, называемых соединениями. Добавить новую стратегию можно нажав на кнопку **Добавить**![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) во вкладке **Общие** и выбрать **Стратегия**. Или нажав правой кнопкой мыши на папке **Стратегии** панели **Схемы**, и нажать на кнопку **Добавить**![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) выпавшем меню. Подробно о **Стратегиях** описано в пункте [Использование кубиков](Designer_Creating_strategy_out_of_blocks.md).

3. Папка **Галерея стратегий** содержит стратегии, на которые вы подписались на панели **Галерея стратегий**. Подробно о **Галереи стратегий** описано в пункте [Галерея стратегий](Designer_Gallery_of_strategies.md).

4. Папка **Торговля** содержит стратегии, которые добавлены для запуска в торговлю. При этом стратегии, которые запущены отмечены значком ![Designer Panel Circuits 02](~/images/Designer_Panel_Circuits_02.png) , а которые остановлены \- отмечены значком ![Designer Panel Circuits 03](~/images/Designer_Panel_Circuits_03.png) . Как добавлять стратегии в папку **Торговля** и как их запустить описано в пункте [Live торговля](Designer_Live_trade.md).

5. Папка **Исходный код** содержит стратегии, которые созданы используя библиотеку для профессиональной разработки торговых роботов на языке C\# [S\#.API](StockSharpAbout.md). Добавить новую стратегию в папку **Исходный код** можно, нажав на кнопку **Добавить**![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) во вкладке **Общие** и выбрать **Исходный код**. Или нажав правой кнопкой мыши на папке **Исходный код** панели **Схемы** и нажать на кнопку **Добавить**![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) в выпавшем меню.

## См. также

[Панель Логи](Designer_Panel_Logs.md)