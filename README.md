# ValutaTrade Hub

Проект реализует сервис хранения и обмена валютами.
Данные курсов берутся из публичных API [CoinGecko](https://www.coingecko.com) и [ExchangeRate](https://www.exchangerate-api.com/).
Пользователь может смотреть обменные курсы валют, покупать, продавать и хранить их в кошельке.

## Возможности

-  Торговля фиатными валютами
-  Торговля криптовалютами 
-  Реальные курсы валют через API
-  Регистрация и аутентификация пользователей
-  Просмотр портфеля с красивыми таблицами
-  Автоматическое обновление курсов

## Структура проекта

```
valutatrade_hub/
├── data/                   # Хранилище данных
│   ├── users.json      # пользователи системы
│   ├── portfolios.json # портфели и кошельки
│   ├── rates.json     # локальный кэш текущих курсов
│   └── exchange_rates.json # исторические данные
├── logs/               # Логи приложения
│   └── actions.log
├── valutatrade_hub/    # Основной код проекта
│   ├── logging_config.py # настройка логирования
│   ├── decorators.py   # декораторы для логирования
│   ├── core/           # Бизнес‑логика
│   │   ├── currencies.py # иерархия валют
│   │   ├── exceptions.py # пользовательские исключения
│   │   ├── models.py   # модели данных (User, Wallet, Portfolio)
│   │   ├── usecases.py # бизнес‑логика операций
│   │   └── utils.py    # вспомогательные функции
│   ├── infra/          # Инфраструктура
│   │   ├── settings.py # Singleton SettingsLoader
│   │   └── database.py # Singleton DatabaseManager
│   ├── parser_service/  # Сервис парсинга курсов
│   │   ├── config.py   # конфигурация API
│   │   ├── api_clients.py # клиенты внешних API
│   │   ├── updater.py  # логика обновления курсов
│   │   └── storage.py  # работа с хранилищем
│   └── cli/
│       └── interface.py  # CLI интерфейс
├── main.py             # Точка входа
├── Makefile            # Автоматизация задач
├── pyproject.toml      # Конфигурация Poetry
└── README.md           # Документация
```

## Установка

## Требования к установке
* **Python** от 3.13;
* **Poetry** от 2.0.0 до 3.0.0;
* **Ruff** от 0.14.7;
* **Requests** от 2.32.5 до 3.0.0;
* **Prettytable** от 3.17.0 до 4.0.0


### API_KEY
Для начала зарегистрируйтесь на сайте [exchangerate-api.com](https://www.exchangerate-api.com/) и получите ключ к API.
 EXCHANGERATE_API_KEY="6eb2459ea00a33c77ac55b54"
---

Задайте переменную среды:                      Пример
export EXCHANGERATE_API_KEY="api_key"          export EXCHANGERATE_API_KEY=6eb2459ea00a33c77ac55b54           
где `"api_key"` - это ваш ключ к API.
---

### Установка
make install

### Запуск 
make project
# или
poetry run python main.py

## Доступные команды Makefile

- `make install` — установка зависимостей через Poetry;
- `make project` — запуск проекта в интерактивном режиме;
- `make build` — сборка пакета для распространения;
- `make publish` — публикация пакета в репозиторий (если настроено);
- `make package-install` — установка собранного пакета через pip;
- `make lint` — проверка кода линтером (ruff).

## Поддерживаемые валюты

### Фиатные
- USD (базовая валюта)
- EUR
- GBP
- RUB
- JPY

### Криптовалюты
- BTC (Bitcoin)
- ETH (Ethereum)
- LTC (Litecoin)
- ADA (Cardano)


## Доступные команды CLI

### Основные операции

```bash
# Регистрация пользователя
register --username <username> --password <password>

# Вход в систему
login --username <username> --password <password>

# Просмотр портфеля (по умолчанию — в USD)
show-portfolio [--base <currency>]

# Покупка валюты
buy --currency <code> --amount <amount>

# Продажа валюты
sell --currency <code> --amount <amount>

# Получение курса между валютами
get-rate --from <currency> --to <currency>
```

### Работа с курсами

```bash
# Обновление всех курсов
update-rates

# Обновление только криптовалют (через CoinGecko)
update-rates --source coingecko

# Обновление только фиатных валют (через ExchangeRate API)
update-rates --source exchangerate

# Просмотр кэшированных курсов
show-rates [--currency <code>] [--top <N>] [--base <currency>]

# Список поддерживаемых валют
list-currencies
```

## Примеры использования

```bash
poetry run project
register --username alice --password secure123
login --username alice --password secure123
show-portfolio --base USD
list-currencies
show-rates --top 3
show-rates --currency BTC --base EUR
get-rate --from BTC --to USD
buy --currency BTC --amount 0.01
buy --currency EUR --amount 1000
show-portfolio
sell --currency BTC --amount 0.005
show-portfolio --base USD
exit
```
# final_project_Ksenofontov_Konstantin_M25-555
