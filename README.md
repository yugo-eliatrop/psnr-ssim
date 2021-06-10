# Приложение для оценки качества видео

Приложение состоит из трех микросервисов: gateway, comparator, dataservice

## Зависимости

Каждый микросервис имеет свои зависимости. Общий список зависимостей всего приложения:

- OC Ubuntu
- Docker
- ffmpeg v4.2.4 и выше
- opencv v4, установленный в режиме совместимости с ffmpeg
- node v14.4.0 и выше
- pm2
- cmake
- make
- СУБД Postgresql v13
- Созданная база данных в соответствии с dataservice/ormconfig.json

## Установка

Каждый микросервис устанавливается отдельно. Процесс установки описан в соответствующих README.md

## Использование

Для запуска микросервисов необходимо запустить брокер сообщений RabbitMQ: `docker run -p 5672:5672 rabbitmq`
Далее запустить каждый микросервис отдельно, сначала gateway для инициализации очередей, затем все остальные.

Для запуска обработки видео необходимо послать POST запрос на порт микросервиса gatawey, например:

Адрес: 

JSON: 
{
  "original": "/home/yugo/Документы/universite/Diploma/videos/web1/2/1080/original.mkv",
  "copy": "/home/yugo/Документы/universite/Diploma/videos/web1/2/1080/vp8realtime.webm",
  "codec": "vp8"
}

где

- original - путь к файлу, сжатому без потерь.
- copy - путь к оцениваемому файлу, сжатому изучаемым кодеком
- codec - название кодека
