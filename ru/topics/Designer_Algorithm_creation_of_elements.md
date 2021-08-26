# Создание алгоритма из кубиков

Для создания схем стратегий и составных элементов, а также тестирования полученных стратегий на исторических данных, можно использовать пример стратегии скользящих средних SMA. Он позволяет пройти полный цикл от создания стратегии, до ее тестирования и отладки. Стратегию скользящих средних SMA можно найти в папке **Стратегии** панели **Схемы**.

1. Создадим новую стратегию как описано в пункте [Использование C\#](Designer_Creating_strategy_from_code.md) из кубиков. Добавить новую стратегию можно нажав на кнопку Добавить ![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) во вкладке **Общие** и выбрать **Стратегия**. Или нажав правой кнопкой мыши на папке **Стратегии** панели **Схемы**, и нажать на кнопку Добавить ![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) в выпавшем меню.

![Designer The creation of a strategy 00](~/images/Designer_creation_of_strategy_00.png)

После нажатия кнопки Добавить ![Designer Panel Circuits 01](~/images/Designer_Panel_Circuits_01.png) в папке **Стратегии** панели **Схемы** появится новая стратегия. В рабочей области появится новая вкладка со стратегией, при переходе на которую в ленте автоматически откроется вкладка **Эмуляция**. На вкладке **Эмуляция** можно изменить название стратегии и дать ей краткое описание.

![Designer The creation of a strategy 01](~/images/Designer_creation_of_strategy_01.png)

2. Для удобной работы стоит раскрыть и зафиксировать панели **Палитра** и **Свойства** области **Схема**, нажав кнопку ![Designer Algorithm creation of cubes 13](~/images/Designer_Algorithm_creation_of_elements_13.png). В результате получится окно следующего вида.

![Designer Algorithm creation of cubes 00](~/images/Designer_Algorithm_creation_of_elements_00.png)

3. Суть стратегии скользящих средних (SMA) заключается в следующем:

- Есть две скользящих средних с разными периодами расчёта, длинная SMA и короткая SMA. В примере кубик [Индикатор](Designer_Indicator.md) длинной SMA называется Long SMA с периодом 80 свечей, короткая SMA называется Short SMA с периодом 10 свечей.
- При пересечении короткой скользящей средней длинную снизу\-вверх, открывать длинную позицию.
- При пересечении короткой скользящей средней длинную сверху\-вниз, открывать короткую позицию.
- При наличии противоположной позиции в момент получения сигнала на открытие позиции, переворачивать позицию.

4. Для всех стратегий необходим инструмент и портфель, по которым будут совершаться сделки. Необходимо добавить их из панели **Палитра** в панель **Дизайнер**. В примере кубик [Переменная](Designer_Variable.md) с типом **Инструмент** называется Security, кубик [Переменная](Designer_Variable.md) с типом **Портфель** называется Portfolio. Установить флажок **Параметры** кубиков Security и Portfolio. При установленном флажке кубик значение будет брать из настроек стратегии. Если флажок параметры не установить, необходимо вручную ввести значения инструмента и портфеля. Если оставить поле **Значение** кубика [Переменная](Designer_Variable.md) пустым и не установить флажок параметры, стратегия при тестировании выдаст ошибку о не установленном значении кубика [Переменная](Designer_Variable.md).

![Designer Algorithm creation of cubes 01](~/images/Designer_Algorithm_creation_of_elements_01.png)

Если в стратегии необходимо использовать несколько инструментов или портфелей, то для каждого кубика необходимо снять флажок **Параметры** и прописать значение инструмента или портфеля.

![Designer Algorithm creation of cubes 02](~/images/Designer_Algorithm_creation_of_elements_02.png)

![Designer Algorithm creation of cubes 03](~/images/Designer_Algorithm_creation_of_elements_03.png)

5. После добавления инструмента и портфеля, следует добавить два кубика [Индикатор](Designer_Indicator.md) выбрать тип SMA, назвать первый Long SMA, установить период 80 свечей, второй назвать Short SMA и установить период 10 свечей.

![Designer Algorithm creation of cubes 04](~/images/Designer_Algorithm_creation_of_elements_04.png)

6. Для работы индикаторов необходимо на них подать серию свечей. Для этого необходимо создать кубик [Свечи](Designer_Candles.md). В примере используется только сформированные свечи с таймфреймом 5 минут.

![Designer Algorithm creation of cubes 05](~/images/Designer_Algorithm_creation_of_elements_05.png)

7. После добавления индикаторов следует добавить два кубика, определяющие пересечения индикаторов. Это кубики [Пересечение](Designer_Crossing.md) из составных элементов. Первый кубик называется Crossing Up. Он определяет пересечение снизу\-вверх. На верхний вход кубика подается индикатор Short SMA, на нижний вход индикатор Long SMA. Оператор CurrComparison устанавливается в значение больше, оператор PrevComparison устанавливается в значение Меньше или равно. Второй кубик называется Crossing Down, он определяет пересечение сверху вниз. На верхний вход кубика подается индикатор Short SMA, на нижний вход индикатор Long SMA. Оператор CurrComparison устанавливается в значение меньше, оператор PrevComparison устанавливается в значение Больше или равно.

![Designer Algorithm creation of cubes 06](~/images/Designer_Algorithm_creation_of_elements_06.png)

8. Для наглядного отображения свечей, индикаторов и сделок стоит добавить [Панель графика](Designer_Panel_graphics.md). В ней добавим элементы отображения, Свечи, два индикатора и сделки.

![Designer Algorithm creation of cubes 07](~/images/Designer_Algorithm_creation_of_elements_07.png)

9. В качестве источника сделок для отображения на графике используется кубик **Сделки** стратегии. В примере называется Strategy trades.

![Designer Algorithm creation of cubes 08](~/images/Designer_Algorithm_creation_of_elements_08.png)

10. Для открытия позиции необходимо добавить два кубика [Регистрация заявки](Designer_Position_opening.md). Первый кубик на покупку рыночной заявкой, на вход которого подается **Инструмент**, сигнал на открытие позиции от кубика пересечения Crossing Up, **Портфель** и объём заявки. Второй кубик на продажу рыночной заявкой, на вход которого подается **Инструмент**, сигнал на открытие позиции от кубика пересечения Crossing Down, **Портфель** и Объём заявки.

![Designer Algorithm creation of cubes 09](~/images/Designer_Algorithm_creation_of_elements_09.png)

11. Соединив линиями ([Линии](Designer_Line.md)) вышеперечисленные элементы, получается схема без учета текущей позиции стратегии. В таком состоянии она будет набирать лишнее количество лотов.

![Designer Algorithm creation of cubes 10](~/images/Designer_Algorithm_creation_of_elements_10.png)

Для контроля позиции необходимо добавить кубик [Позиция](Designer_Position.md), на вход которого подается **Инструмент** и **Портфель**.

![Designer Algorithm creation of cubes 11](~/images/Designer_Algorithm_creation_of_elements_11.png)

Для обработки текущей позиции можно воспользоваться уже готовой схемой, описанной в пункте [Определение объема позиции](Designer_Determination_of_volume_position.md). Эта схема определяет фактическое значение необходимого объема для выставления в заявке. И при необходимости переворота позиции она подаст удвоенное значение портфеля.

12. В результате законченная стратегия имеет вид:

![Designer Algorithm creation of cubes 12](~/images/Designer_Algorithm_creation_of_elements_12.png)

## См. также

[Создание составных элементов](Designer_Creating_composite_elements.md)