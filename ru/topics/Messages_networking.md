# Сетевое взаимодействие

Для организации взаимодействия по сети можно использовать связку компонентов [FIX протокол](Fix.md). [FixMessageAdapter](../api/StockSharp.Fix.FixMessageAdapter.html) обеспечивает трансляцию FIX\-сообщений в сообщения [S\#](StockSharpAbout.md). [FixServer](FixServer.md) позволяет выполнять обратную операцию. Это обеспечивает совместимость сообщений этих типов. 

Следовательно, если требуется куда\-то транслировать сообщения или организовать взаимодействие по сети с использованием команд, то можно использовать данный подход.