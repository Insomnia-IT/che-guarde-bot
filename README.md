# che-guarde-bot
Телеграм бот для администрирования канала посольства и чата комментариев. Оригинальный проект находится [тут](https://github.com/Novartole/che-guarde-bot).

Original source code and english version of this doc can be found [here](https://github.com/Novartole/che-guarde-bot).

## Проблема
Хочется сохранить в канале возможность комментировать без того, чтобы добавляться в чат. Следовательно чат обязательно должен быть без заявок на вступление. Но без заявок могут попасть левые и увидеть закрытую информацию из телеграм-канала. 

Кроме того, один из пунктов - удаление из чата при удалении из канала. Задумка, что у всех кто в чате должна быть подписка на канал. Вышел из канала - потерял возможность и в чате быть. Обратной связи нет. Из чата можно самостоятельно выйти, оставшись в канале.

## Решение
Придумался такой бот-модератор. Вступить могут все у кого есть ссылка, но чужаки быстро удаляются и банятся.

![telegram-cloud-photo-size-2-5355336890104007911-y](https://github.com/Insomnia-IT/che-guarde-bot/assets/33791946/a9385c01-85f8-4886-a762-8dfccc33ea0c)

# Разработка
Для запуска локально обязательны несколько переменных:
- CHANNEL_ID - id канала,
- CHANNEL_CHAT_ID - id чата комментариев,
- WORK_CHAT_ID - id рабочего чата, в который будут приходить уведомления,
- TELOXIDE_TOKEN - токен телеграм бота.
Id чатов и канала можно получить, [например](https://stackoverflow.com/questions/72640703/telegram-how-to-find-group-chat-id), с помощью веб-версии телеграма. Токен выдается специальным ботом под названием [BotFather](https://telegram.me/BotFather).

Эти переменные могут быть переданы как явно, так и через конфиг файл. Например, если в корне есть файл .env.local, то вызов будет следующий:
```rust
CONFIG_PATH=".env.local" cargo run
```

Если приложение запускается в дебаг профиле, то владелец бота, при записи своего пользовательского id в переменную MAINTAINER_ID, может вызывать дополнительные полезные команды, помогающие при разработке. Полный список команд можно посмотреть, отослав запущенному боту команду /help.

Логирование можно поднастроить стандартной переменной RUST_LOG. Пример использования можно посмотреть в файле .env.example в корне проекта.

Проверить доступность бота можно командой /ping, которая доступна для всех пользователей. Она должна быть отослана в личной беседе боту. Если бот доступен, он отвечает *pong*.
