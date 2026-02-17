# Telegram бот

Простой бот на Python с командами `/start`, `/help` и анализом лотов по ссылкам.

## Установка

1. Создайте виртуальное окружение (рекомендуется):

```bash
cd telegram-bot
python3 -m venv venv
source venv/bin/activate   # macOS/Linux
```

2. Установите зависимости:

```bash
pip install -r requirements.txt
```

## Токен бота

1. Откройте [@BotFather](https://t.me/BotFather) в Telegram.
2. Отправьте `/newbot` и следуйте инструкциям.
3. Скопируйте выданный токен.

## Запуск

Задайте токен и запустите бота:

```bash
export TELEGRAM_BOT_TOKEN="ваш_токен_от_BotFather"
python bot.py
```

Или в одну строку:

```bash
TELEGRAM_BOT_TOKEN="ваш_токен" python bot.py
```

## Команды бота

- `/start` — приветствие
- `/help` — справка
- `/post текст` — рассылка сообщения всем (только для администратора)
- **Ссылка на лот ТБанкрот** (tbankrot.ru) — бот загружает страницу и через ChatGPT оценивает, можно ли считать лот на 100% неликвидным
- Любой другой текст — бот просит отправить ссылку на лот (tbankrot.ru или fedresurs.ru)

## Анализ лотов ТБанкрот (ChatGPT)

Чтобы бот анализировал ссылки на лоты с сайта [tbankrot.ru](https://tbankrot.ru):

1. Получи API-ключ OpenAI: [platform.openai.com/api-keys](https://platform.openai.com/api-keys).
2. Задай переменную окружения при запуске:

```bash
export OPENAI_API_KEY="sk-..."
TELEGRAM_BOT_TOKEN="..." BOT_ADMIN_IDS="..." python bot.py
```

3. Пользователь должен быть подписан на канал. Отправь боту сообщение со ссылкой на лот (например `https://tbankrot.ru/...`). Бот загрузит страницу, извлечёт текст и отправит его в ChatGPT с просьбой определить: можно ли на 100% считать лот неликвидным. Ответ придёт в чат (вердикт ЛИКВИДНЫЙ / НЕЛИКВИДНЫЙ / НЕЯСНО и краткое обоснование).

## Рассылка поста всем подписчикам

1. Узнай свой Telegram ID (например, у [@userinfobot](https://t.me/userinfobot)).
2. При запуске бота задай переменную `BOT_ADMIN_IDS` — твой ID (или несколько через запятую):

```bash
export TELEGRAM_BOT_TOKEN="ваш_токен"
export BOT_ADMIN_IDS="123456789"
python bot.py
```

3. В Telegram напиши боту: **`/post Ваш текст сообщения`** — это сообщение получит каждый пользователь, который хотя бы раз писал боту (нажимал /start, писал сообщения или нажимал кнопки). Обычные пользователи не могут использовать `/post`.

## Дальнейшее развитие

В `bot.py` можно добавить:
- новые `CommandHandler` для своих команд;
- `MessageHandler` с другими фильтрами;
- кнопки (`InlineKeyboardButton`, `ReplyKeyboardMarkup`);
- работу с базой данных или API.
