1) Создать форк репозитория https://gitlab.com/anestesia.loc/bookstore (или просто стащить и создать из него свой отдельный)
2) Написать:
- jenkins pipeline для сборки docker image приложения (опционально - сделать автоматический запуск, если в репозитории изменился Dockerfie и файлы приложения)
- jenkins pipeline для деплоя приложения с помощью docker compose (сборка должна принимать как параметр значение docker image и делать оповещение через Telegram Bot`a о результате - успех/неуспех)
- jenkins pipeline для проверки работоспособности задеплоенного приложения (обычным курлом можно дернуть эндпоинт /healthcheck) - job должен запускаться автоматически после деплоя и только если деплой прошел успешно
- jenkins pipeline для снятия дампов с БД приложения по расписанию


У меня на канале есть немного видосов про Jenkins
- https://youtu.be/jv917Nzdcf4
- https://youtu.be/pMw4novPDxE
- https://vkvideo.ru/video-224078601_456239038
