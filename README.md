# User API

## Описание

Приложение со слоистой архитектурой для управления пользователями 
с JWT-аутентификацией.

Для хранения используется класс Store, 
подключение к которому происходит через контекстный менеджер.  
После перезапуска сервера память очищается. 

Используются два метода аутентификации - через middleware и dependencies.  
Авторизация доступна как по username, так и по email.

---

## Архитектура проекта

- **apps/**  
  - **auth/** — модули для аутентификации и авторизации
  - **user/** — модули для пользователей  
- **core/** — основные компоненты и утилиты приложения  
- **routers/** — маршруты API  
- **settings/** — конфигурация приложения  
- **utils/** — вспомогательные функции и валидаторы  
- **main.py** — точка входа в приложение  
- **pyproject.toml** — настройки проекта  
- **README.md** — документация

---

## Активация и запуск проекта

1. Клонировать репозиторий:
    ```bash
    git clone https://github.com/SlavaKlkv/fastapi_2.git
    ```
2. Перейти в корень проекта:
   ```bash
    cd fastapi_2
   ```
3. Создать файл переменных окружения  
    Например, .env с содержимым:
    ```
    PRODUCTION=False
    
    DB_HOST=localhost
    DB_PORT=5432
    DB_USER=user
    DB_PASS=pass
    DB_NAME=db
    
    SECRET_KEY=your_secret_key
    ALGORITHM=HS256
    ACCESS_TTL_MIN=15
    REFRESH_TTL_DAYS=7
   ```
4. Установить зависимости:
   ```bash
    poetry install
   ```
5. Активировать виртуальное окружение:
   ```bash
    poetry env activate
   ```
6. Запустить сервер с автоперезапуском:
   ```bash
    uvicorn main:app --reload
   ```

---

## Запросы

  ### Открыть Swagger UI - http://127.0.0.1:8000/docs

  ### - Необходимо зарегистрироваться
  **POST** `/api/v1/auth/register`
  
  Пример тела запроса:
  ```json
  {
    "username": "string",
    "email": "user@example.com",
    "password": "string1",
    "full_name": "string"
  }
  ```
  
  Ответ:
  ```json
  {
    "username": "string",
    "email": "user@example.com",
    "full_name": "string",
    "id": 1,
    "disabled": false
  }
  ```

  > **/api/v1/auth/login** — стандартный вход через **form-data**, используется для кнопки **Authorize**.  
  > **/api/v1/auth/login_json** — возвращает данные о пользователе и токенах.

  ### - Дальше нужно авторизоваться через `Authorize 🔒`.

  ### - Получить список пользователей по id (когда уже есть минимум трое)
  **GET** `/api/v1/users`

  Parameters  
  *Add integer item* `1`  
  *Add integer item* `3`
  
  Ответ:
  ```json
  {
      "users": [
        {
          "username": "string",
          "email": "user@example.com",
          "full_name": "string",
          "id": 1,
          "disabled": false
        },
        {
          "username": "string3",
          "email": "user@example.com",
          "full_name": "string",
          "id": 3,
          "disabled": false
        }
      ]
  }
  ```

---

## Дополнительные инструменты

- Найти и исправить ошибки:
    ```bash
    poetry run ruff check --fix .
    ```
  
- Отформатировать код по PEP8:
    ```bash
    poetry run ruff format .
    ```
  
---

## Лицензия
MIT
