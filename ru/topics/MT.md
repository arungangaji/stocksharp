# S\#.MT4 и S\#.MT5

[S\#](StockSharpAbout.md) имеет интеграцию с терминалами MT4 и MT5 через специальные коннекторы. Для установки данных коннекторов необходимо использовать [S\#.Installer](SharpInstaller.md) (подробнее, [Установка и удаление программ ](Installer_installing_removing_programs.md)).

Оба коннектора используются одинаково, поэтому ниже будет описал процесс подключения к MT4:

### Настройка MT коннектора

Настройка MT коннектора

1. Установка MT коннектора необходимо сделать в папку *C:\\Users\\%ваш\_ник\_юзера%\\AppData\\Roaming\\MetaQuotes\\Terminal\\%много\_букв\_и\_цифр%\\MQL4\\Experts\\* (в случае MT5 путь будет содержать MQL5). Структура в итоге должна выглядеть следующим образом (корневая директория содержит MQL скрипт и MT коннектор, под\-папка StockSharp необходимые S\#.API файлы):

   ![MT 0](~/images/MT_0.png)
2. Запустить терминал MT и подключиться к торгам.
3. В меню Tools\-\>Options выбрать вкладу **Experts Advisors** и убедиться, что включено разрешение для торговли внешним dll (**Allow DLL imports**):

   ![MT 1](~/images/MT_1.png)
4. В случае, если при установке коннектора (пункт 2) терминал был запущен, то необходимо обновить список экспертов, нажав правой кнопкой на Experts и выбрав в меню **Refresh**:

   ![MT 2](~/images/MT_2.png)
5. Выбираем S\# эксперт, нажимаем правую кнопку и выбираем в меню пункт **Attach to a chart**:

   ![MT 3](~/images/MT_3.png)
6. Появится окно с настройками, где можно задать логин\-пароль (по\-умолчанию включена анонимная авторизация), а так же адрес подключения (в случае подключения сразу к нескольким терминалам адреса должны содержать уникальные порты).
7. На графике (выбирается первый попавшийся) справа вверху должна появится иконка смайлика:

   ![MT 4](~/images/MT_4.png)

   А также в окне логов эксперта должна появиться информация об успешном запуске скрипта, количество инструментов.
8. Если не получена лицензия MT4 или MT5, то в логе появится похожая на следующую строка:

   ![MT 5](~/images/MT_5.png)
9. Подключение к МТ идет по FIX протоколу, и используется коннектор [FIX протокол](Fix.md). В качестве демонстрации использована программа [S\#.Terminal](Terminal.md). Ниже настройки для транзакционного подключения и подключения с маркет\-данными (в случае MT5 порт по\-умолчанию равен 23001 вместо 23000):

   ![MT 6](~/images/MT_6.png)

   ![MT 7](~/images/MT_7.png)

   Аналогичные настройки необходимо сделать в [S\#.Designer](Designer.md), [S\#.Data (Hydra)](Hydra.md) или любых S\#.API программах.

   Логин и пароль оставляются пустыми в случае анонимной авторизации (пред. пункт). В случае подключения к МТ несколькими роботами, необходимо указывать уникальный логин для идентификации разных подключений.

   > [!TIP]
   > - Скрипт необходимо запускать перед подключением StockSharp к МетаТрейдеру и не останавливать его, пока это подключение необходимо.  
   > - Чтобы в StockSharp видеть исторические свечки, их необходимо выгрузить с сервера МетаТрейдера. Как это сделать, читайте в документации самого МетаТрейдера.

   В случае успешного подключения пример должен показать список инструментов и счетов:

   ![MT 8](~/images/MT_8.png)
10. В случае возникновения ошибок ведутся логи коннектора, которые доступны в папке **Experts\\StockSharp\\Data\\Log**:

    ![MT 9](~/images/MT_9.png)