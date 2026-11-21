# maxapi

![Логотип проекта](logo.png)

`maxapi` — Python-библиотека для разработки чат-ботов под API мессенджера MAX. Она предоставляет классы `Bot` и `Dispatcher`, набор типизированных моделей, фильтры, маршрутизацию событий и готовые интеграции для webhook-сценариев.

## ✨ Возможности

- Работа с long polling через `Dispatcher.start_polling(...)`.
- Работа с webhook через `aiohttp`, `FastAPI` и `Litestar`.
- Методы для сообщений, чатов, участников, файлов и подписок.
- Декораторы событий и фильтры для роутинга обновлений.
- Контексты и state machine в модуле `context`.
- Утилиты для форматирования, команд, медиа и inline-кнопок.
- Набор тестов в каталоге `tests/`.

Документация проекта и дополнительные примеры указаны в исходном README: [love-apples.github.io/maxapi](https://love-apples.github.io/maxapi/).

## 🚀 Быстрый старт

Локальная копия проекта оформлена как Python-пакет с `pyproject.toml`, поэтому базовая установка выполняется так:

```bash
cd maxapi
python -m pip install .
```

Отдельной команды запуска у библиотеки нет: после установки она используется из собственного Python-кода.

## 📁 Структура проекта

- `maxapi/` — исходный код библиотеки.
- `maxapi/bot.py` — основной класс `Bot` и высокоуровневые методы API.
- `maxapi/dispatcher.py` — диспетчер, роутеры и запуск polling/webhook.
- `maxapi/types/` — типизированные модели сообщений, чатов, пользователей и обновлений.
- `maxapi/methods/` — реализации методов API MAX.
- `maxapi/webhook/` — интеграции webhook для разных фреймворков.
- `tests/` — тесты проекта.
- `pyproject.toml` — метаданные пакета, зависимости и настройки инструментов.

## 🛠 Использование

Токен бота можно передать явно в `Bot(token="...")` или через переменную окружения `MAX_BOT_TOKEN`. Пример запуска polling по мотивам исходного README:

```python
import asyncio
import logging

from maxapi import Bot, Dispatcher
from maxapi.types import Command, MessageCreated

logging.basicConfig(level=logging.INFO)

bot = Bot()
dp = Dispatcher()

@dp.message_created(Command("start"))
async def hello(event: MessageCreated):
    await event.message.answer("Привет из maxapi!")

async def main():
    await dp.start_polling(bot)

if __name__ == "__main__":
    asyncio.run(main())
```

Для webhook в библиотеке предусмотрены:

- `await dp.handle_webhook(...)` для `aiohttp`;
- модули `maxapi.webhook.fastapi`;
- модули `maxapi.webhook.litestar`.

Если у бота уже созданы webhook-подписки, исходный README рекомендует удалить их через `await bot.delete_webhook()` перед запуском polling.

## 🧪 Технологии

- Python
- aiohttp
- pydantic
- backoff
- magic-filter
- aiofiles
- puremagic
- FastAPI
- Litestar
- uvicorn
- pytest
- Ruff
- mypy

Оригинальный автор библиотеки: Denis.

Подпись относится к текущей версии проекта.

---

Автор: legenda  
Telegram: [@LEGENDA_SD](https://t.me/LEGENDA_SD)
