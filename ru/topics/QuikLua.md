# Настройка Quik Lua

Предпочтительным режимом подключения к терминалу Quik является использование скрипта Lua. Ниже описан процесс установки и настройки скрипта. 

## Процесс установки и настройки

1. **Только для QUIK 7\!** Скачать и установить [Visual C++ Runtime x86](https://aka.ms/vs/16/release/vc_redist.x86.exe) (необходимо скачать vcredist\_x86.exe).
2. Загрузить скрипт StockSharp.Quik.lua, который находится в папке *References*. Рядом с файлом скрипта должны быть все необходимые сборки.

   В файле скрипта можно указать порт, на котором сервер будет принимать подключения, а так же логин и пароль, с которыми будет подключаться клиент, если поле логин не указано, то подключение может выполняться от имени любого пользователя. По умолчанию используется порт 5001 и отсутствует проверка логина:

   ```none
   			-- Настройки QUIK Lua Fix сервера
   			-- Серверный порт, на котором будет работать FIX сервер.
   			ServerPort=5001
   			-- Логин, с которым разрешено подключение к FIX серверу.
   			-- ServerLogin="quik"
   			-- Пароль, с которым разрешено подключение к FIX серверу.
   			-- ServerPassword="quik"
   			-------------------------------------------------------------------------
   			
   ```

   Файл скрипта так же содержит настройки записи отладочной информации, уровень записываемых сообщений и путь к файлу логов:

   ```none
   			-- Настройки логирования
   			-- Уровень логирования.
   			-- 1 - Debug
   			-- 2 - Info
   			-- 3 - Warning
   			-- 4 - Error
   			LogLevel=2
   			-- Название текстового файла (без расширения), 
   			-- в который будут сохраняться лог-сообщения.
   			LogFile="StockSharp.QuikLua"
   			-------------------------------------------------------------------------
   			
   ```
3. Далее необходимо загрузить скрипт в терминале Quik.
   1. Открываем таблицу доступных скриптов (Сервисы \- Lua скрипты \- Доступные скрипты).
   2. Выбираем кнопку "Добавить".
   3. После добавления скрипта, его необходимо запустить.

   ![QuikLua](../images/QuikLua.png)

   Запуск скрипта выполняется один раз, при следующем запуске терминала скрипт будет запущен автоматически.
4. Мониторинг работы Lua скрипта.

   Для мониторинга работы скрипта (после его запуска в Quik) в папке со скриптом будет создан лог\-файл (по умолчанию *StockSharp.QuikLua.log*). В этом файле показаны основные запросы клиента к серверу и ошибки обработки данных в скрипте.
